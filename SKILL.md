---
name: weekly-grocery-list
description: >
  Generates a personalized weekly grocery list with meal suggestions, organized
  for Amazon Fresh delivery or Whole Foods pickup in Arlington, MA.
  Re-run each week for a fresh, varied plan.
---

# Weekly Grocery List Generator

## Purpose

Generate a **new, varied weekly grocery list** every time this skill is invoked. The list should feel fresh — don't repeat the same meals week after week. Rotate cuisines, proteins, and seasonal produce. The output should be practical, organized, and ready to shop.

---

## User Profile

- **Location**: Arlington, MA 02476
- **Preferred store**: Amazon Fresh (delivery to Arlington, MA)
- **Backup option**: Whole Foods Market — 808 Massachusetts Ave, Arlington, MA 02476 (open daily 8AM–9PM, in-store pickup available)
- **Household size**: 1 person
- **Diet**: Omnivore — no strict dietary restrictions, but strong preference for **whole, organic, and minimally processed foods**. Avoid highly processed ingredients, artificial additives, refined sugars, and ultra-processed packaged foods.
- **Shopping priorities**: Healthy & nutritious — prioritize nutrient-dense whole foods, quality proteins, healthy fats, and plenty of fresh vegetables and fruits.

---

## Weekly Grocery List Output Format

When invoked, generate a complete grocery list structured as follows:

### 1. This Week's Meal Plan (Brief Overview)

List **5 dinner ideas** for the week. Each dish that is cooked should last for two meals so this list shoudl cover roughly 10 total meals. Also suggest:
- A **salad** tub of organic salad that will last for the week
- **healthy fruits** for making fruit salads and smoothies. This should cover 2-3 servings of fruit per day
- **crepe** should be made of eggs, coconut milk, whole wheat flour, and hazelenut spread 

Vary by:
- Protein sources (wild-caught fish, pastured poultry, grass-fed beef, eggs, legumes)
- Cuisine style (Mediterranean, Asian, Mexican, Middle Eastern, American, etc.)
- Cooking method (sheet pan, stovetop, grain bowl, salad, slow-cook, etc.)
- Carbs including brown rice, vegetables as a side, white pasta, and tortilla chips

All meals should be built around **whole, minimally processed ingredients** — real food that a home cook would recognize.

### 2. Grocery List (Organized by Department)

Group items into the following categories for easy shopping:

**🥩 Meat & Seafood**
**🥛 Dairy & Eggs**
**🥦 Produce**
**🥫 Fruit**
**🍞 Carbs**
**❄️ Frozen**
**🧴 Household / Other**

For each item, include:
- Quantity or approximate amount (e.g., "1 lb", "2 bunches", "1 carton")
- A note if it's for a specific meal (optional but helpful)

### 3. Shopping Guidance

At the end, include a short section:
- **Amazon Fresh tip**: Note any items that are particularly good value or commonly stocked on Amazon Fresh (e.g., pantry staples, bulk items).
- **Whole Foods tip**: Note any items better sourced at Whole Foods (e.g., specialty cheeses, specific organic produce, fresh-baked bread, prepared foods from the hot bar for a quick night).
- **Estimated weekly spend**: Give a rough ballpark for the full list (low/medium/high range is fine).

---

## Variation & Freshness Rules

To ensure the list feels new each week, the skill MUST:

1. **Rotate proteins** — I try and use a 60/40 ratio of white meat to red meat on my meals per week. Try and stick to this ratio if possible but small deviations isn't a big deal. 
2. **Include at least one adventurous or seasonal recipe** each week.
3. **Follow a strict organic only rule for vegetables and fruit** — This should apply to salad, vegetables, and fruit purchased. 
4. **Avoid dairy entirely with only one exception** - Every month, purchase a small carton of organic milk for omlettes. Otherwise, coconut milk should be purchased every week for smoothies and crepes. 
5. **Don't repeat last week** — if the user mentions what they had recently, avoid repeating it.
6. **Organic first** — default to organic for everything, especially the Dirty Dozen: strawberries, spinach, bell peppers, grapes, tomatoes, peaches, apples, celery, cherries, pears, nectarines, blueberries.
7. **No ultra-processed items** — never include processed deli meats, packaged snack foods with long ingredient lists, refined grain products, sodas, or products with added sugars as a primary ingredient.
8. **Wild caught fish** only
9. **Occassionaly include ice cream** - ice cream should be included once every 3 weeks. 

---

## Invocation Instructions

When a user says something like:
- "Generate my grocery list for this week"
- "What should I buy this week?"
- "Give me a new grocery list"
- "Time to restock"

…execute this skill immediately. Do NOT ask clarifying questions before generating — just produce the full list. The user can ask for adjustments after seeing the first draft.

**Optional inputs the user may provide (incorporate if given):**
- Dietary restrictions or preferences this week (e.g., "no red meat this week")
- What's already in the fridge/pantry (to avoid redundant purchases)
- Budget constraints (e.g., "keep it under $100")
- Number of nights they're cooking vs. eating out
- Specific craving or cuisine they want

---

## Example Invocation Response Structure

```
## 🛒 Your Weekly Grocery List — Week of [Date]

### This Week's Meal Plan

**Dinners:**
1. [Meal name] — [1-sentence description]
2. ...

**Lunches:** [Quick overview]
**Breakfast:** [Staple for the week]
**Snack/Treat:** [One fun item]

---

### Grocery List

**🥩 Meat & Seafood**
- [ ] 1.5 lbs boneless chicken thighs (for meals 1 & 3)
- [ ] 1 lb salmon fillets (for meal 4)
- ...

**🥛 Dairy & Eggs**
- [ ] 1 dozen eggs
- ...

[...continue for all departments...]

---

### Shopping Guidance

**Amazon Fresh**: Best for ordering [pantry items, bulk staples, etc.]. Use Subscribe & Save on [item] if you go through it weekly.

**Whole Foods (808 Mass Ave, Arlington)**: Worth stopping in for [specialty item]. Their [department] is especially good.

**Estimated spend**: ~$[X]–$[Y] for the week
```

---

## Tone & Style

- Be practical and concrete — this is a real shopping list, not a recipe blog
- Keep meal descriptions short (1–2 sentences max)
- Use checkboxes `[ ]` for every grocery item so the user can tick things off
- Be friendly and slightly enthusiastic — grocery planning should feel fun, not tedious
- If it's a holiday week or notable time of year, acknowledge it (e.g., "It's February — let's do something cozy")

---

## Store Reference

| Store | Address | Hours | Use For |
|-------|---------|-------|---------|
| Amazon Fresh | Delivery to Arlington, MA | Order anytime, delivery windows vary | Primary weekly shop, pantry staples, bulk |
| Whole Foods Market | 808 Massachusetts Ave, Arlington MA 02476 | Daily 8AM–9PM | Specialty items, fresh bread, hot bar, organic produce |

---

*Skill created for Arlington, MA — last updated February 2026.*
