# Problem Statement: Reach Together (`fresher_track`)

## Objective
Build a clean, user-friendly web or mobile application that connects students traveling to the same destination (e.g., heading to the airport, railway station, concert, or going home for the weekend) so they can travel together, share cab fares, and feel safer.

The challenge focuses on **clean user experience (UI/UX), intuitive trip discovery, and practical student safety features**.

---

## Target Environment & Stack Freedom
* **Platforms:** Web application (responsive mobile-web) or native mobile app (React, Vue, Next.js, Flutter, React Native, etc.).
* **Target Audience:** College students / freshers traveling with luggage, late-night transit, or daily campus commuters.

---

## Core Features to Build
1. **Trip Posting & Discovery:**
   * **Post a Trip:** Users can create an upcoming ride (Origin, Destination, Date/Time window, and available seats).
   * **Find Trips:** Search trips heading to the same destination/hub within a similar time window (e.g., departing within $\pm 30$–$60$ minutes).
2. **Travel Pool Formation & Capacity:**
   * Display open travel pools with visual seat indicators (e.g., "2 of 4 seats open").
   * Join request flow: Co-travelers can request to join a pool, and the host can accept or decline.
   * Auto-lock: Disables join requests once the vehicle reaches full capacity (e.g., max 4 passengers).
3. **Simple Fare Split Calculator:**
   * Shows an estimated total ride cost and automatically calculates each person's share as new members join the pool.
4. **Safety & Privacy:**
   * Contact details (phone number/full address) remain hidden until the host approves the travel request.

---

## Brownie Points Feature (Bonus)
* **★ Women-Only Travel Pools:** A dedicated safety filter and toggle allowing female students to create and discover **exclusive female-only travel groups** for late-night rides or transit safety. Non-eligible profiles cannot see or request to join these pools.

---

## Hard Requirements
1. **Functional Trip Matching:** Searching for trips must match both the destination area and overlapping departure time windows.
2. **Interactive Seat Capacity:** Seat availability must update dynamically when a member is added, and the app must prevent overbooking.
3. **Clean & Responsive UI/UX:** The interface must be visually polished, intuitive for first-time users, and responsive on mobile screens.
4. **Privacy Protection:** Personal contact numbers must remain masked until a travel request is approved by the host.

---

## Strictly Prohibited
* **NO Static Non-Interactive Mockups:** The app must be functional (creating a trip in one browser tab/device must be searchable and joinable from another).
* **NO Unmasked Contact Leaks:** User contact details must not be publicly exposed to strangers on the open search feed.
* **NO Overbooking:** The pool must not allow more passengers than the specified vehicle seat capacity.
