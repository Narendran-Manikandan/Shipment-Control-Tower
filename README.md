# Global Shipment Control Tower (demo)

A demo of a shipment control tower with sample data, hosted as a static page.

- `index.html` is the whole app.
- `users.js` is the list of people who can sign in (email, role, hashed password).
- `make-users.html` creates `users.js`, one user at a time or from a filled-in `users-template.csv`. Open it on your own computer, not from the website.

This is a demo with sample data. The sign-in is a gate for a demo, not real security: `users.js` is public, so use throwaway passwords and never enter real company information. Each person's data is kept in their own browser and is not shared with other people. The app runs on the real date and time, and the sample data is dated from the day it is first opened.

To share data between devices, run `supabase-setup.sql` once in a free Supabase project, then enter the project URL and public key in `make-users.html` and upload the new `users.js`. Without it, each device keeps its own copy.

## What this build can do
- **Users** (Administration, Users and roles): create Internal, Carrier, Warehouse, External Logistics Partner and Partner Executive users with phone and location. With shared data on, each gets a sign-in with a temporary password, and the person must choose their own at first sign-in.
- **Passwords**: My profile and Change password for everyone; an admin can Reset password or make a one-time Reset link; a partner can do the same for its own executives.
- **users.js**: Administration, Go live, Publish users to GitHub. Paste a fine-grained access token (Contents: Read and write, this repository only) once per session and every user change updates `users.js` for you. The token is never stored.
- **Roles and access**: View, Create, Edit and Delete per module (Shipments, Warehouse Operations, Freight Cost, Analysis, Users, Settings). Create profiles such as Finance, SCM, Warehouse Manager or Admin in one click.
- **External Logistics Partners**: linked to a shipper and/or receiver, with their own executives (My team). They see and work only on those shipments and cannot open warehouse operations, analysis, freight cost, Administration or Settings.
- **Warehouse type**: Distribution Center, Manufacturing Site, Research Center or Supplier, in the list, the filters and shipment creation.
- **Data backup** (Administration, Settings): Export all data as a ZIP of separate files or one JSON file, and Upload dump to restore everything, with a confirm summary first and a success summary after.

This is a demo with sample data. The sign-in is not real security: users.js is public and anyone with the shared database key can change its data, so use throwaway passwords and no real company information.


## New in this version
- **Reports page** (Insights): the Daily Status Report in your DSR template layout (34 columns), plus the shipment register, overdue milestones, shipments at risk, free time, delivery schedule, slot requests, data quality, carrier scorecard, Pending Invoices, Payment Pending, freight spend, RG Pending and the Monthly RG Accrual. Excel or CSV. Which role can download which report is set in Administration, Role Access, Report Access.
- **Freight Audit** (Commercial and Access): delivered shipments where your company pays the freight. Record actual freight cost, carrier invoice number and remarks; status Invoice Pending, Payment Pending or Paid.
- **RG Pending** (Operations, Logistics Analyst by default): DAP and DDP need only a Final RG after delivery; other terms need an In-Transit RG (with optional TO and PL#) once in transit, then a Final RG. Download the pending report, fill it in, upload it back.
- **Track & Trace access** is now editable per role (Role Access).
- Quick-filter switches above the monitor: Missing Docs only, Delayed only, Pending RG only.
- Account menu: Compact Table Rows, and Theme (match device, light or dark).
- Titles and subheadings use headline-style capitalisation.
- Optional shipping documents with a Missing Docs badge (run supabase-storage-setup.sql once for shared storage), and a Quotation ID on quotes.
- Sidebar sections open and close; profile, password, problem report and sign-out are in the avatar menu at the top right.
