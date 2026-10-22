# Leilon Alchemy Engine

A full-stack, two-sided web application designed for tabletop RPGs (D&D 5e) to manage custom alchemy, foraging, and inventory mechanics for the *Shadows of Second Chance* campaign.

## Features

### Player Side
* **My Reagents:** View ingredients discovered in-game, sorted by biome. Unknown traits display as `???`.
* **Interactive Foraging:** Roll a simulated d20 Search check based on ingredient rarity DCs, followed by a d4 Yield check if successful. Includes skill modifiers (Nature/Survival).
* **Taste Testing:** Sample ingredients by rolling a d20 Constitution check to uncover the first hidden trait or suffer an effect. 1 unit is consumed per test.
* **Brewing Station:** Combine two ingredients with a solvent tier (Level 1 Impure, Level 2 Pure, Level 3 Pristine). Matching traits yield potions; mismatches yield Foul Sludge. 1 unit of each ingredient is consumed per brew.
* **Inventory Management:** Players can track their ingredient quantities, add custom amounts (e.g., from purchases), and track their character bonuses.

### Dungeon Master (DM) Side
* **Campaign Dashboard:** Manage up to 5 campaigns, view active players, and inspect their skill modifiers.
* **Live Activity Log:** Real-time tracking of player actions, including foraging yields, taste test outcomes, potion brewing results, and manual inventory adjustments.
* **Anti-Cheat Architecture:** The Supabase backend uses Row Level Security (RLS) and RPCs to ensure players only see what they have discovered or harvested.

## Deployment Guide

This application requires a Supabase backend to store ingredients, players, and inventory securely. 

### Prerequisites
1. A free [Supabase](https://supabase.com/) account.
2. A static web host (e.g., GitHub Pages, Netlify, Vercel, or local browser).

### Backend Setup (Supabase)
1. Create a new Supabase project.
2. Navigate to the **SQL Editor**.
3. Copy and paste the contents of `database-schema.sql` (or the complete sequence of updates) and click **Run**. This will create the required tables (`players`, `ingredients`, `inventory`, `activity_logs`, etc.), setup Row Level Security (RLS) policies, and define the necessary RPC functions (e.g., `p_forage_harvest`, `p_brew`).

### Frontend Setup
1. Open `index.html`.
2. Locate the following lines near the top of the `<script>` tag:
   ```javascript
   const SUPABASE_URL = "PASTE_YOUR_SUPABASE_URL_HERE";
   const SUPABASE_ANON_KEY = "PASTE_YOUR_SUPABASE_ANON_KEY_HERE";
