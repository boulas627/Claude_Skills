---
name: date-night-finder
description: >
  Finds the top 3–6 date night options (drinks + dinner) near a given location.
  Filters out overly expensive venues and presents results on an interactive map.
  Trigger when a user asks for date night ideas, restaurant + bar combos, or
  romantic evening plans and provides a town, city, or zip code.
---

# Date Night Finder

## Purpose

Given a location (city, town, or zip code), surface the **best 3–6 date night
venues** — places that do both drinks and dinner well — within **5 miles**.
Skip anything in the top 20 % most expensive tier (no Michelin-star tasting
menus, no ultra-premium cocktail bars).  Present results visually on a map with
brief, personal-feeling notes for each spot.

---

## Step-by-Step Workflow

### 1 · Confirm the Location

If the user provided a specific city/town/zip, use it directly.  If the location
is ambiguous (e.g. "Springfield"), ask which one before proceeding.

### 2 · Search for Candidate Venues

Run **multiple `places_search` queries** to cast a wide net.  Good query
templates (substitute the actual location):

```
"romantic restaurants [city]"
"cocktail bar and dinner [city]"
"wine bar restaurant [city]"
"date night restaurant [city]"
"gastropub [city]"
"craft cocktail dinner [city]"
```

Use `max_results: 6` per query and set `location_bias_lat/lng` to the
coordinates of the supplied location with `location_bias_radius: 8000` (≈5 mi).

Collect all unique results (deduplicate by `place_id`).

### 3 · Filter the Candidate List

From the raw results, **exclude** any venue that matches one or more of these
signals:

| Signal | Why |
|--------|-----|
| Price level = 4 (Google's "$$$$") | Top 20 % expensive — skip |
| Primarily a fast-food or fast-casual chain | Not date-night appropriate |
| No mention of a bar / cocktails / wine | Drinks component missing |
| Permanently closed | Obvious |

Keep only venues with price level 1–3 ($ / $$ / $$$).  If price level is
missing from the data, make a best-effort judgment from the venue name and
category.

### 4 · Score and Rank the Shortlist

Rank surviving candidates by a simple composite:

1. **Rating** (highest weight) — Google rating ≥ 4.0 preferred
2. **Review count** — more reviews = more confidence
3. **Vibe fit** — bonus points for places explicitly tagged as "romantic",
   "cozy", "date night", or that offer both a full bar and a dinner menu
4. **Distance** — all else equal, prefer closer

Pick the **top 3–6** from this ranked list.

### 5 · Write Venue Notes

For each selected venue write a short (2–3 sentence) note that covers:
- What makes it special for a date night
- Signature drinks or food style
- Any practical tips (reservations, best nights, parking, etc.)

Keep the tone warm and personal, not like a Yelp review.

### 6 · Display on Map

Call `places_map_display_v0` in **markers mode** with all selected venues.
Pass the `place_id` exactly as returned by `places_search`.
Include the venue note in the `notes` field.

### 7 · Brief Follow-Up

After the map, write 2–4 sentences summarising the selection and inviting the
user to ask for more details on any spot or to adjust criteria (e.g. "more
casual", "closer to downtown", "vegetarian-friendly").

---

## Pricing Philosophy

The goal is **accessible but special** — venues where a couple can enjoy real
cocktails and a satisfying dinner without bill shock.  Think:

- ✅  A neighbourhood wine bar with small plates
- ✅  A lively gastropub with craft beer and a proper kitchen
- ✅  A midrange Italian with a good Aperol spritz list
- ❌  A $350/head omakase
- ❌  A hotel rooftop bar where a cocktail is $28+

When in doubt, lean toward including a venue rather than excluding it — the
user can always filter further.

---

## Example Trigger Phrases

- "Find me date night spots in Austin, TX"
- "What are good places for drinks and dinner near 02134?"
- "I'm taking my partner out in Chicago — any ideas?"
- "Date night options in Burlington, Vermont?"

---

## Error Handling

| Situation | Response |
|-----------|----------|
| Fewer than 3 venues found after filtering | Relax the distance to 8 miles and re-run one more search pass |
| Location not found | Ask the user to clarify (full city + state, or zip) |
| All results are $$$$ | Explain the constraint, ask if user wants to loosen it |
| No cocktail/bar options in results | Try additional queries: "wine bar [city]", "speakeasy [city]" |

---

## Evals

```json
[
  {
    "id": "eval-0",
    "prompt": "Find me the best date night spots for drinks and dinner in Somerville, MA.",
    "expectations": [
      "Returns 3 to 6 venues",
      "All venues have a price level of $ $$ or $$$  — none are $$$$",
      "Each venue includes a short personal note explaining why it's good for a date",
      "Results are displayed on a map using places_map_display_v0",
      "Venues are within approximately 5 miles of Somerville MA"
    ]
  },
  {
    "id": "eval-1",
    "prompt": "Date night ideas near zip code 78701.",
    "expectations": [
      "Returns 3 to 6 venues",
      "No ultra-premium fine dining (no $$$$)",
      "Map is shown with all venues",
      "Venues combine a drinks offering with dinner",
      "Results are in or near Austin TX (78701 is downtown Austin)"
    ]
  },
  {
    "id": "eval-2",
    "prompt": "I want to take my girlfriend somewhere nice in Burlington, Vermont — drinks and dinner, nothing too expensive.",
    "expectations": [
      "Recognises Burlington VT as the location",
      "Returns 3 to 6 venues",
      "Excludes top-tier expensive venues",
      "Includes venue notes with date-night flavour",
      "Displays a map"
    ]
  }
]
```
