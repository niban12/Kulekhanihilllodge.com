# Kulekhani Hill Lodge — Connected Demo

Prepared by JARVIS Agency. This is a proposed demonstration, not a replacement recommendation and not connected to the lodge's existing application or production records.

## Requirements
- Node.js 18 or newer
- No npm packages are required

## Run locally
1. Extract the ZIP folder.
2. Open a terminal in the project folder.
3. Run `npm start` (or `node server.js`).
4. Open `http://localhost:3000` for the customer website.
5. Open `http://localhost:3000/staff` for the separate staff portal.

The first run creates `data/db.json` with clearly labelled sample records. The server persists changes in that file across refreshes and restarts.

## Demo sign-in
- Manager username: `demo.manager`
- Reception username: `demo.staff`
- Password for either demo identity: `KulekhaniDemo2026!`

These are public demonstration credentials, not production credentials. Do not deploy this demo publicly as-is. Authentication is a simple in-process demo session and role check; it is not a production identity system. Session tokens are held in server memory, so a server restart signs users out.

## Main features
- Customer-facing responsive lodge concept site, separate from staff portal.
- Demo accommodation records and clearly marked illustrative photography.
- Booking inquiry form with server-side validation, unique reference and persistent save.
- Limited inquiry status lookup that exposes only basic status/stay details.
- Staff sign-in/sign-out and separate management interface.
- Shared booking inbox, inquiry status changes, internal notes and reservation creation.
- Server-side overlap checks for room reservations, check-in/check-out controls and cancellation.
- Room management (manager demo role), calendar, guest directory, stock movements, housekeeping/maintenance task statuses, CSV reports, activity history and reset function.
- Persistent JSON data store with sample records; no third-party packages or external services required.

## Honest limitations / pre-launch work
- This is a local demonstration, not a production-ready hotel PMS. It uses a JSON file rather than a transactional database; concurrent writes and multi-instance deployments are not supported.
- Demo sign-in credentials are visible in the README and login screen. Replace with a real identity provider, hashed credentials, secure cookies, CSRF protections, rate limiting, stronger authorization and security review before deployment.
- Public inquiry endpoint has basic validation but no production-grade spam/rate protection.
- No email/SMS is sent, no payments are taken, and there is no live integration with the lodge's existing software.
- Photos on the public website are illustrative third-party landscape/room imagery, not verified photographs of Kulekhani Hill Lodge. Labels disclose this; replace with approved property photography and attribution before publication.
- Room names, capacities, rates, facilities, inventory, guests, and reservations are all sample data. Confirm all property facts, policies, location pin, rates and contact channels with the lodge.
- The customer-facing status lookup relies on a hard-to-guess reference but has no secondary verification. For production, add email/OTP or equivalent guest verification.
- Staff role separation is limited to manager vs reception for room edits. Detailed role-based permissions and managed staff accounts are not production-complete.
- No actual availability guarantee is made for unassigned room-category requests. The conflict checker applies to assigned room reservations.
- Accessibility and responsive layouts are implemented as a starting point but still require manual cross-browser, keyboard and assistive-technology QA.

## Quick test checklist
1. Start server; open `/` and `/staff`.
2. Submit a valid inquiry from the public form and note the reference.
3. Sign in at `/staff`, open Booking inquiries, and locate the same reference.
4. Change inquiry status/add internal notes and save.
5. Create a reservation from the inquiry by assigning a room. An overlapping reservation for the same room should be rejected by the server.
6. Refresh the staff page and confirm saved data persists.
7. Record stock in/out from Inventory & stock; check the new quantity.
8. Use Settings & audit to reset starter demo records.

## Architecture
- `public/index.html`, `public/app.js`, `public/styles.css`: customer experience.
- `public/staff.html`, `public/staff.js`: private staff experience.
- `server.js`: built-in Node HTTP server, API validation, demo auth, reservation overlap rules, shared data operations.
- `data/db.json`: persistent local demonstration database created on first run.

Integration with the lodge's existing system requires technical verification and explicit authorization from the lodge and its software provider where applicable.
