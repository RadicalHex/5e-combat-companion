# Changelog

## v1.7.0 — 2026-03-06

### Class Resources System
- New **Class Features** section in ⚙ Settings — enable resource blocks for class-specific abilities; set max values per feature; toggles and config inputs update live
- **Class Resources** panel block renders between Attacks and Spell Slots when any feature is enabled; returns nothing if all features are off (no orphan divider)
- Settings section is **collapsible** (▸/▾ toggle) so it doesn't crowd future settings additions
- Three display types: **pip rows** (click to spend/restore), **pool rows** (+/− buttons), **toggle rows** (Available/Spent)
- **Pact Magic** integrates inside the Spell Slots section with its own pip row and slot-level label rather than appearing in the Class Resources panel
- **Short Rest** restores: Channel Divinity, Action Surge, Second Wind, Superiority Dice, Ki Points, Wild Shape, Pact Magic
- **Long Rest** restores all features to their configured max

### Features shipped (all base classes + key subclasses)
| Class | Feature | Type |
|---|---|---|
| Bard | Bardic Inspiration | Pips + die label |
| Cleric / Paladin | Channel Divinity | Pips |
| Cleric / Paladin | Lay on Hands | Pool (HP) |
| Cleric / Paladin | Divine Smite | Slot-level calculator |
| War Domain | War Priest | Pool |
| Fighter | Action Surge | Pips |
| Fighter | Second Wind | Pip + die label |
| Battle Master | Superiority Dice | Pips + die label |
| Fighter 9+ | Indomitable | Pips |
| Barbarian | Rage | Pips |
| Rogue | Sneak Attack | Reference (dice count display) |
| Monk | Ki Points | Pool |
| Druid | Wild Shape | Pips |
| Wizard | Arcane Recovery | Toggle (Available/Spent) |
| Divination Wizard | Portent | Pips |
| Sorcerer | Sorcery Points | Pool |
| Wild Magic Sorcerer | Tides of Chaos | Toggle |
| Warlock | Pact Magic | Pips (in Spellcasting section) |
| Warlock | Mystic Arcanum | Pips |
| Artificer | Flash of Genius | Pool |

---

## v1.6.0 — 2026-02-28

### Active Effects — Full Overhaul (both trackers)
- **No more popups** — clicking **+** instantly creates a "New Effect" card with the name field pre-selected and ready to type; no prompt dialog anywhere in the flow
- Double-click any effect name to rename it inline (Enter / Escape to confirm or cancel)
- Each effect card now has an expandable **description** section — click **▼** to open, double-click the text to edit in a textarea, Save / ✕ to confirm or discard
- **C pip button** replaces the concentration confirm dialog — toggle concentration on/off per effect; activating one automatically clears concentration from any other effect
- Descriptions persist to localStorage; existing effects are migrated automatically with empty descriptions
- **HP Effects** (Aid, Heroes' Feast, Max HP −) now live under their own collapsible sub-header, independently collapsible from the Manual Effects list

### Actions Section (both trackers)
- Actions section now has a **collapse chevron** — click the header to hide all action cards
- Each action card now has an expandable **description** — click **▼** to open, double-click to edit inline, same pattern as feats and inventory
- `talent-companion.html`: section label corrected from "Attacks" to "Actions"

### Polish
- `tracker.html`: HP bar label corrected from "Base Form" to "HP"

---

## v1.5.0 — 2026-02-28

### Attack Dice Roller
- Each custom attack card now has two inline roll buttons: **🎲 [modifier]** (to hit) and **🎲 [dice expression]** (damage)
- Button labels show the actual values at a glance — `🎲 +7` and `🎲 2d6+3` instead of generic labels
- Clicking a button rolls instantly and displays the result inline on the card
- To Hit shows a single total; Damage shows a full breakdown (e.g. `[4+2]+3 = 9 slashing`)
- Results clear automatically when the attack is edited or removed
- **Nat 20**: gold `⚔️ CRITICAL HIT!` toast + card result highlighted in bright gold
- **Nat 1**: red `💀 CRITICAL MISS...` toast + card result highlighted in red
- Powered by `parseDiceExpr()` — regex parser handles `+7`, `1d8+3 fire`, `d4`, and anything in between
- Ported identically to `talent-companion.html`
- Fully offline — pure JS, no external calls

## v1.4.1 — 2026-02-28

### Offline Support
- Cinzel and Inter fonts are now **embedded locally** — the tracker is fully functional with no internet connection (contributed by Spirutural via PR #3)

### Bug Fixes
- `talent-companion.html`: Short Rest rolled-phase modal now guards with an explicit `srPhase === 'rolled'` check, preventing stale renders if the state machine is interrupted mid-flow

---

## talent-companion v1.0.0 — 2026-02-27

### The Talent's Companion — New File
- New single-file tracker (`talent-companion.html`) on the `talent-companion` branch, tailored to **The Talent** psionic class (MCDM / Matthew Colville)
- Based on `tracker.html` v1.4.0 — all base features preserved
- Storage key: `talent_companion_v1` (separate from main tracker)

### Strain Tracker
- Three strain rows — **Body** (pink), **Mind** (cyan), **Soul** (violet) — each with 8 brain pip slots
- Click a pip to set strain directly; **+/−** buttons for manual adjustment
- Total Strain / Strain Maximum display — **pulses red** when within 2 of maximum, shows ⚠ MAXIMUM REACHED when at limit
- Strain Max and Manifestation Die are click-to-edit inline
- Long rest now resets strain and concentration instead of spell slots

### Psionics Powers System
- **103 powers** hardcoded from The Talent rulebook across 6 schools: Chronopathy, Metamorphosis, Pyrokinesis, Resopathy, Telekinesis, Telepathy
- **Manage Powers** button opens a searchable modal — filter by name or school, check to add powers to your active list
- **Active Powers List** — compact cards showing order, school, manifestation time, concentration status
- Concentration toggle per power — tracked for Manifestation Score calculation

### Manifestation Resolver
- **Manifest** button on any power card opens a step-by-step resolver modal
- Shows Manifestation Score (order + extra concentrating powers)
- Roll the die yourself or let the tracker roll for you
- Color-coded results: 🟢 No strain / 🟡 +1 strain / 🔴 +order strain
- Strain Allocation step — distribute gained strain across Body/Mind/Soul before confirming
- Special warning when strain would exceed maximum — choose to manifest and die, or cancel

### Effects Section (replaces Active Spells)
- **Status** panel renamed to **Effects**
- **Strain Conditions** auto-populate as colored badges based on current strain values (12 threshold conditions across Body/Mind/Soul)
- **Manual Effects** sub-panel replaces Active Spells — same free-text entry, dismissable, works as before

### Formulas Update
- Formulas dropdown now shows **Power Attack** (d20 + INT Mod + Proficiency) and **Power Save DC** (8 + INT Mod + Proficiency) with live calculated values instead of generic Spell Attack/Spell Save DC

---

## v1.4.0 — 2026-02-27

### Lore Book
- New **📖 Lore** floating panel — open from the header button
- Create named pages for NPCs, locations, factions, session notes, etc.
- Page dropdown to switch between pages; **+** to add, **✎** to rename, **✕** to delete
- Freeform textarea per page — content auto-saves to localStorage
- **Export** downloads a standalone `lore-book.json`; **Import** restores from file
- Panel is draggable, resizable (8-handle), and minimizable — same controls as the stat block viewer
- Lore Book entry added to the **?** help guide

### Saves
- **Flat bonus per save** — click **✏** on the Saves section to enter edit mode and set a per-save bonus
- Stacks on top of your ability modifier and proficiency (for items like Ring of Protection, Good Luck Stone, Cloak of Protection)
- Active bonuses shown in **amber** next to the save total

### Left Column — Collapsible Sections
- **Character**, **Stats**, **Ability Scores**, and **Saves** sections are now individually collapsible
- Click the section title or the **▲/▼** chevron to toggle; collapse state persists across reloads
- Clicking **✏** on a collapsed section auto-expands it before entering edit mode

### Polish & Fixes
- Lore panel titlebar buttons (minimize/close) now styled correctly — were showing browser-default white background
- Saves section title was permanently showing the Save button due to a `null` key bug — fixed
- Section title chevrons: resolved a double `style` attribute bug that was preventing `justify-content: space-between` from applying; chevrons now sit flush right, matching all other collapsible sections
- Edit pencil button opacity raised from 0.4 → 0.65 for better visibility at rest

---

## v1.3.0 — 2026-02-26

### Hit Dice
- **Hit Dice tracker** added below the HP bar — collapsible, heart-pip display (♥ = available, ♡ = spent)
- Set max dice and die type (d6 / d8 / d10 / d12) via inline controls when expanded
- Click a filled heart to spend a die; click an empty heart to restore one

### Magic Item Charges
- Magic items now support an optional **charge tracker** — set a max via a number input in the expanded item section
- Amber pip row (⚡ ●●●○○) appears inline below the item name when charges are enabled
- Click any pip to spend down to that point or restore up to it
- Charges are fully manual — no automatic restoration on rest

### Skills
- **Flat bonus** per skill — click the calculated skill value to set an additional modifier (for racial bonuses, item bonuses, etc.)
- Skill pip turns **red** when a flat bonus is active, making overrides visible at a glance

### Inventory
- **Click item name** to expand/collapse its description — no need to find the ▶ button
- Item rename now requires **double-click** to prevent accidental prompts

---

## v1.2.0 — 2026-02-26

### Feats
- New **Feats** section in the right panel between Inventory and Skills
- Add feats by name; expand to view or edit a description
- Double-click the description or feat name to edit inline
- Section is independently collapsible; state persists in localStorage

### Conditions Reference
- **Conditions ▾** dropdown added to the header
- Lists all 15 SRD conditions (Blinded through Unconscious) with rules-as-written mechanical effects
- Scrollable, closes on click-outside

### Inventory
- Item descriptions now support **double-click to edit** — ✏ Edit button removed

---

## v1.1.0 — 2026-02-26

### Inventory Consolidation
- Merged **Inventory**, **Magic Items**, and **Attuned Items** into a single unified **Inventory** panel
- Items now carry a type (`normal` / `magic`) — magic items show Equipped and Attuned toggles inline
- Attuned sub-section with pip display sits below the item list; attunement slot cap still adjustable
- Full data migration from old localStorage shape — existing saves upgrade automatically

### Spellcasting
- Spell Save DC, Spell Attack, and Ability selector now **collapse with the Spell Slots panel** — no more values floating above the fold when slots are hidden

### Status Panel
- **Active Spells sub-section is now independently collapsible** — collapse state persists in localStorage

### Materials Viewer
- Replaced the standalone **Materials** button and the **Stat Blocks** tab bar with a single **Materials ▾** dropdown
- Clicking Materials always opens the floating viewer (ready for drag-and-drop)
- Dropdown lists all loaded stat blocks; clicking one activates it and brings the panel forward
- Loading a new file via **+ Add file…** opens the viewer automatically
- Viewer panel can still be closed independently via its own controls

### Help Guide
- Added **?** button to the header that opens a quick-start guide modal covering all major sections

## v1.0.0 — 2026-02-26

First full-featured release.

### HP & Status
- HP Effects section: Aid, Heroes' Feast, and Max HP Reduction — each correctly adjusts current and/or max HP per 5e rules, with editable values and ON/OFF toggles
- Active Spells and Conditions merged into a unified collapsible **Status** panel

### Stats & Skills
- Saving throws now have **3-state proficiency pips** (none / proficient / expertise)
- Full **Skills section** with auto-calculated modifiers, 3-state pips, and support for custom skills
- Level & Class label moved to the **header subtitle** (click to edit)
- **Passive Perception** moved into the Stats block
- **Speed** now expandable to show Walk / Swim / Climb / Fly

### Spellcasting
- Spell Ability, Spell Save DC, and Spell Attack moved to the top of the **Spell Slots** panel with their own pencil-edit mode
- Spellcasting section removed from the left panel

### Inventory
- **Quantity +/− buttons** on all inventory and magic items
- **Item descriptions** — collapsible per item, with read-only view and pencil edit
- **Currency tracker** (PP / GP / SP / CP) at the bottom of Inventory
- **Attunement slot cap** now has both − and + buttons

### Layout & Polish
- Right column widened to 360px default
- Stat panel can no longer be dragged off the top of the screen
- Spell DC/Attack labels now show `(auto)` instead of a cryptic icon
