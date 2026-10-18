# Kulekhani Hill Lodge — JARVIS Agency Demo

A runnable, two-part hospitality demonstration: public customer website + separate staff portal, sharing one local persistent JSON data store. This is a proposed demo only; it is not connected to Kulekhani Hill Lodge's live software and is not a production PMS.

## Requirements
- Node.js 18 or newer
- No npm packages required

## Run locally
1. Extract the ZIP.
2. Open a terminal in the `kulekhani-lodge-demo` folder.
3. Run `npm start` (or `node server.js`).
4. Open `http://localhost:3000` for the public customer website.
5. Open `http://localhost:3000/admin` for the separate staff portal.

## Demo staff sign-in
- Username: `demo.manager`
- Password: `LodgeDemo2026!`

This is a shared demonstration credential, not a production account. Do not expose this local demo to the public internet as-is. Change the demo credential and add a production identity provider, CSRF protection, rate limiting, HTTPS, database backups and security review before any real deployment.

## What works
- Responsive customer website navigation: Home, About, Accommodation, Gallery, Location & Contact, Booking Inquiry.
- Inquiry form validation, unique reference, duplicate-submit suppression within 60 seconds, local persistent storage, and confirmation that does not falsely claim a reservation is confirmed.
- Status lookup requires both inquiry reference and the email address submitted with it; only status, dates and requested category are returned.
- Separate staff portal with server-checked sign-in, HttpOnly session cookie, protected admin API routes and sign-out.
- Dashboard metrics calculated from stored records; recent activity log.
- Inquiry search/filter/review, status updates, staff notes, date editing, room assignment and overlap conflict checks for confirmed room assignments.
- Guardrails on check-in/check-out transitions.
- Room record editing and active/inactive state.
- Inventory stock-in, stock-out and adjustment transactions with quantity validation and history.
- Housekeeping / maintenance task status and notes.
- Guest directory derived from demo inquiries.
- Calendar view, summary reports and CSV exports.
- Reset demo data action.
- JSON data persists to `data.json` across refreshes and server restarts.

## Important limitations
- This is a lightweight local demonstration built with Node.js built-in modules and a JSON file, not a production database. Concurrent writes, backups and multi-server deployment are not supported.
- The session store is in server memory and sessions end when the server restarts. The shared demo credential is not appropriate for production. Role-based permissions beyond a single demo administrator are not implemented.
- No email, SMS, payment processing, live availability, or external property-management-system integration is configured.
- Guest status lookup is a demo flow using reference + email, not a high-assurance production verification mechanism.
- Inventory items, tasks, rooms, room details, capacity, and rates are sample records, not verified lodge facts.
- Official phone/email, exact location pin, business hours, room inventory, facilities, and policies need confirmation from the client.
- Landscape and accommodation imagery from Unsplash are explicitly illustrative reference images, not claimed to be photos of the lodge. Replace them with client-approved, licensed property images before public use. The image URLs require an internet connection.
- Google Fonts and remote images require internet access. The core application/server itself uses no npm dependencies.
- No formal security audit or production readiness review has been performed.

## Architecture
- `server.js`: HTTP server, public API, inquiry validation, demo sign-in, protected staff API, availability conflict checks and persistent storage.
- `public/index.html`: shared application shell.
- `public/styles.css`: responsive visual system.
- `public/app.js`: customer and staff user interfaces, client-side navigation, forms and staff workflows.
- `data.json`: created automatically on first run and holds the shared demo records.

## End-to-end test performed
A local smoke test was performed during packaging:
1. `/api/health` returned `ok: true` and identified the JSON-file demo store.
2. Public website returned the HTML shell.
3. Demo staff sign-in succeeded and returned a session cookie.
4. A booking inquiry was submitted through the public API and received a generated `KHL-...` reference.
5. The same reference was visible in the authenticated staff data response.
6. Demo data was reset after the test.

This was a server/API smoke test, not a full browser-based accessibility, cross-device or penetration test. Perform additional testing in the target browser before presenting to the client.

## Client and integration note
The lodge reportedly already uses a booking/stock application that staff are satisfied with. This demo is intended to help evaluate a possible guest website and operational workflows, not to assert a need to replace that system. Any integration would require technical discovery, authorization and cooperation from the current software provider where applicable.
