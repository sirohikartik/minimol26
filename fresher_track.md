# Problem Statement: Reach Together (`fresher_track`)

## Objective
Build a web or mobile application that connects people traveling to the same destination (e.g., students heading to the airport, railway station, concert, or commuting home) so they can travel together, share rides/fares, and ensure personal safety.

The application must dynamically match users based on **route corridor overlap, flexible departure time windows, and trust/safety preferences**, rather than basic exact-destination string matching.

---

## Target Environment & Stack Freedom
* **Platforms:** Web application (responsive mobile-web) or native mobile app (React Native, Flutter, Swift, etc.).
* **Target Audience:** College students / freshers traveling with luggage, late-night transit, or daily campus commuters.

---

## Core Functional Capabilities
1. **Spatio-Temporal Trip Matching Engine:**
   * Matches travelers not just by identical endpoints, but along **overlapping route corridors** (e.g., picking up a co-traveler along the way within a maximum acceptable detour tolerance).
   * Supports **flexible departure windows** (e.g., *"departing between 4:00 PM and 4:30 PM"*).
2. **Dynamic Travel Groups & Capacity Management:**
   * Once a match is found, creates an ephemeral travel pool with strict capacity limits (e.g., 3-4 passengers for a cab/auto).
   * Includes an interactive approval workflow (host/group can accept or decline join requests).
3. **Safety & Preference Guardrails:**
   * Allows users to set safety filters (e.g., gender-preferred travel groups for late-night transit, verified campus email requirement).
   * Emergency/safety sharing: one-click trip itinerary and live tracking link shareable with trusted contacts.
4. **Automated Fair Fare Splitting:**
   * Calculates dynamic cost-per-person based on pickup/drop-off distances or equal split, generating payment breakdown summaries.
5. **Real-Time Group Coordination:**
   * Live in-trip coordination: shared meeting point selection, group chat/status updates, and departure countdown.

---

## Brownie Points Feature (Bonus)
* **★ Women-Only Travel Pools:** A dedicated safety filter and verification workflow allowing female travelers to create and join **exclusive female-only travel groups** for late-night journeys, airport cabs, or transit safety. Non-eligible users cannot see or request to join these pools.

---

## Hard Requirements
1. **Algorithmic Corridor Matching:** The search engine must calculate spatial proximity (e.g., bounding boxes or route proximity) and time overlap. It cannot rely on naive exact string equality of location names.
2. **Real-Time Group State Sync:** When a user requests to join a pool, acceptances, rejections, and capacity state changes must update in real time across all members' devices without requiring manual page reloads.
3. **Privacy by Default:** Exact pickup addresses and personal phone numbers must remain masked until both parties mutually accept the travel match.
4. **Responsive Mobile-First UX:** The app must be fully optimized for mobile devices, supporting instant trip posting and 1-tap join requests on the go.

---

## Strictly Prohibited
* **NO Naive String-Only Matching:** Searching for trips cannot just check `if (trip.destination === user.destination)`. It must account for coordinate distances and departure time windows.
* **NO Fake Static Mock Data:** Submissions must demonstrate live interactive matching where creating a trip on User Device A appears in real time in search results on User Device B.
* **NO Unauthenticated Open Contact Leaks:** User contact details or live coordinates must not be publicly exposed to unmatched users.
* **NO Overbooking:** The system must strictly enforce vehicle capacity limits and reject join requests once a pool is full.
