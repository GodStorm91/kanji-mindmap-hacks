# ⚔️ Product Requirements Document: Kanji Ronin (Kanji Duel)

## 1. Executive Summary
**Kanji Ronin** is a competitive turn-based mobile web game where players duel by chaining Kanji characters based on shared components (radicals). It gamifies the "structural analysis" of Kanji, turning rote memorization into a high-stakes tactical battle.

> **Concept:** "Shiritori" (Word Chain) meets "Chess Clock" logic, applied to Kanji radicals.

## 2. Core Gameplay Loop

### The Duel
1.  **Setup:** 2 Players (PvP) or Player vs Bot (PvE).
2.  **Start:** The system deals a random "Root Component" (e.g., 氵 - Water).
3.  **Turn Action:**
    *   Player 1 must input a Kanji containing 氵 (e.g., **海** - Sea).
    *   System decomposes **海** into `{氵, 毎}`.
4.  **The Pivot (The Hook):**
    *   Player 2 receives the previous Kanji (**海**) and must reply with a Kanji sharing *any* component from it.
    *   P2 can reply with **池** (matches 氵) OR **梅** (matches 毎).
    *   *Strategy:* P2 chooses **梅** (Plum) to shift the battlefield from "Water" to "Tree" (木).
5.  **Win Condition:**
    *   Opponent runs out of time (Chess Clock).
    *   Opponent cannot find a valid Kanji.
    *   Opponent repeats a used Kanji (Duplicate).

### The Chess Clock
*   Each player has a **Total Time Bank** (e.g., 3 minutes).
*   Time counts down only during your turn.
*   **Blitz Mode:** 10s per turn + 1m bank.

## 3. Features & Scope

### Phase 1: MVP (Minimum Viable Product)
*   **Platform:** Mobile Web (PWA).
*   **Mode:** PvE (vs Bot) & Local PvP (Pass & Play).
*   **Dictionary:** Common Joyo Kanji (~2136 characters).
*   **Data Source:** `kradfile` (Kanji Radical Database) logic.
*   **UI:** Minimalist vertical interface. Dark mode. Large Kanji display.

### Phase 2: Multiplayer & Meta
*   **Online PvP:** Real-time matchmaking via WebSockets.
*   **Ranked Ladder:** Ashigaru → Samurai → Daimyo → Shogun.
*   **"Mindmap" Integration:**
    *   When a player is stuck, they can spend "Karma" to view a **Mindmap Hint** (pulling data from this repo's `maps/`).
    *   *Monetization/Hook:* Unlock cool visual mnemonics.

## 4. Technical Architecture

*   **Frontend:** React (Next.js) + Tailwind CSS (for UI) or Phaser (for effects).
*   **Backend:** Node.js (Game Server) + Redis (State management).
*   **Database:**
    *   **Static:** JSON dump of KRADFILE (Component decomposition).
    *   **Dynamic:** User profiles, match history (PostgreSQL/Firebase).
*   **Validation Logic:**
    *   Input: `梅`
    *   Prev: `海` (`氵`, `毎`)
    *   Decomp(`梅`) = `木`, `毎`
    *   Intersection = `毎` -> **VALID**.

## 5. UI/UX References
*   **Vibe:** Sumi-e (Ink wash painting), parchment paper textures, sharp katana sound effects on valid submission.
*   **Input:** Custom Kanji handwriting recognition (ideal) or IME Keyboard (MVP).

## 6. Success Metrics
*   **Retention:** Average matches per user per day.
*   **Education:** "I learned a new radical because I got beaten by it."

## 7. Roadmap
- [ ] **Week 1:** Prototype the "Component Matcher" script (JS/Python).
- [ ] **Week 2:** Basic UI (Single player vs Dummy Bot).
- [ ] **Week 3:** Integrate specific "Mindmap Hacks" as hints.
