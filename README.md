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


## What is new in this release
- **Four document upload fields** on the shipment entry form and in the shipment details: Shipment Invoice, Packing List, BL / HAWB / AWB and Others (with a description). Several files per field, each file gets the type of its field, and a checklist shows which of the three key documents are attached. The carrier invoice stays in Freight Audit.
- **Milestone Management** shows the HBL first with the internal reference small, a compact References column (MBL, invoice, container, with +n for several), a search box, and a Show Reference Numbers switch. Carrier Updates has the same. Download Overdue now has HBL, MBL and Container Number instead of Tracking Number, and the upload finds a shipment by HBL or MBL when the Shipment Reference is empty (an HBL on two shipments is rejected, never guessed).
- **Delivery slots by warehouse type.** Distribution Centers keep the slot grid. For Manufacturing Sites, Research Centers and Suppliers the carrier requests a delivery day (with an optional second choice and a preferred time of day), and the receiving team confirms the date and time, proposes another date or time, or rejects it. Slot settings and blocked slots show only for Distribution Centers. Requests already made are unchanged.
- **Hamburger menu.** On phones and tablets the menu is a drawer that opens showing the section headings; tap a heading to see its pages, one section at a time. On desktop the same button collapses the sidebar to an icon strip (remembered per device).
- **Settings section** holds Administration (Logistics Manager and Logistics Analyst by default, extendable in Role Access). The old "Commercial and Access" section is now **Freight Cost**.
- **Headline-style capitalisation** for every tile title and table heading, and for the headings of the report downloads (units such as kg stay lowercase, and phrases such as Picked Up and Log In are handled). The Daily Status Report keeps your template's headings exactly.

## Stabilisation release (read this before going live)
- **Much faster pages with lots of data.** A check that ran on every page was repeating work once per shipment. At 1,000 shipments the slowest page went from 2.5 seconds to 0.5; at 2,000 shipments from 9.6 seconds to 1.3.
- **Live Mode** (Administration, Go Live). Turn it on when real work starts. It hides the demo date, Preview as, Reset demo data, the demo guide and every Load sample history button, and sample history can no longer be loaded. Turn it off to bring them back.
- **Company time zone.** "Today" now follows the company time zone, Asia/Kolkata by default, so the header date and the app's date agree at all hours (before, between midnight and 05:30 in Chennai the app counted the previous day). To change it, add "timezone":"Asia/Kolkata" (any zone name) to your users.js. Warehouse local times and scheduled reports still use the true UTC moment.
- **Shipment Monitor switches** can no longer trap you: they stay visible when nothing matches, the empty message says why and has a Clear Filters button, each switch shows how many shipments it would show, and there is one Delayed only control.
- **Phones:** the Add item line row on the entry form is two columns on a phone and three on a tablet, so the fields are usable.
- **Damaged saved data:** if the data saved in the browser cannot be read, a red message stays on screen, a copy of the damaged data is kept on the device, and it can be downloaded.
- **Data Size card** (Administration, Go Live) shows how much data you hold against the roughly 5 MB browser limit.
- **Safer downloads:** CSV cells that start with = + - or @ can no longer run as Excel formulas.
- **Double-clicking Upload** no longer attaches a document twice.
- **Permissions** are now also checked inside the Go Live group, Remove logo, Remind all, and sample history actions.
- **Screen reader labels** added to the monitor status filter, the user form, and others.

## New in this version
- **Carrier Performance is cleaner.**
  - The cluttered "On-Time Delivery and Pickup by Carrier" chart and the 15-line monthly chart are replaced by **Monthly Trend by Carrier**. Choose the measure (on-time delivery, on-time pickup, or shipments delivered), the carriers to compare (Top 5 by default, with All and None), a From and To month, and whether to show all carriers combined. View it as a chart (each carrier has its own colour and its name at the end of the line) or as a table with green and red cells against the target. Months with fewer than 3 shipments for a carrier are shown hollow in the chart and marked * in the table, so one late shipment does not look like a collapse. With fewer than 3 months in view it opens as a table.
  - A new tile, **Picked up on time**, shows the share of shipments picked up on or before the planned pickup date. Click it to see the shipments with planned and actual pickup and how early or late.
  - The **Carrier Scorecard** has a Pickup on time column (shown for information; the Score is unchanged), and so does the Carrier Scorecard report.
  - **Data Quality** flags a carrier name spelled two ways (for example FedEx and Fedex), without changing your data.
- **RG is now tracked for every PO and item line.** The RG Pending page shows, for each line, the HBL, MBL, invoice number, container, PO number, item number, quantity and the **required milestone** (In-Transit RG, Final RG, or Final RG only for DAP and DDP), with the received quantity for each milestone.
  - One shipment can have several RG numbers, and one RG number can cover several lines or POs of the same shipment.
  - A line can be received in parts: each RG has its own quantity, and the milestone is complete when the full quantity is received.
  - Mark a line **NA** with a remark when no RG is needed. NA needs no RG number or date and counts as complete.
  - Tick lines of one shipment and choose Record RG, or use the shortcuts for all lines or all lines of one PO.
  - The same RG number on two shipments asks for confirmation first (it is normally used on one shipment).
  - The RG Pending Report is now one row per pending line, with columns to fill in (RG number and date, quantity, TO, PL#, remarks) for each milestone. Type NA with a remark for lines that need no RG. Upload it back on the RG page; a preview shows what it understood before anything is saved. Repeating an RG number on several rows makes one RG.
  - The Monthly RG Accrual report is one row per line of each RG, with its quantity. NA lines are left out.
  - RG records from the earlier version convert automatically to cover every line of the shipment at its full quantity.
- **Duplicate shipment invoices are refused.** If the same shipper has already entered an invoice number on another live shipment, the new entry is rejected (single entry, bulk upload, and Edit Shipment). Spaces, dots, hyphens, slashes and capitals are ignored when comparing. The same invoice number from a different shipper is accepted, and a cancelled shipment's invoice number can be used again. Many item lines on one shipment can share an invoice number. Existing duplicates are not deleted; they appear in Data Quality as "Duplicate invoice number".
- **Freight Audit upload.** On the Freight Audit page, Download Template gives the Pending Invoices Report with fillable columns (Carrier Invoice No., Invoice Date, Freight Charge, Additional Charges and type, Payment Status, Payment Date, Hold and reason, Remarks). Fill it in and use Upload Invoice Details. Shipments are found by HBL, then MBL, then internal reference. One invoice covers one HBL, and a second invoice on the same HBL goes on another row. A row with only the invoice number and Paid with a date marks an existing invoice paid. The Payment Pending Report also has Payment Status and Payment Date columns for marking invoices paid. A preview shows new, updated, marked-paid, blank and problem rows before anything is saved, and problem rows can be downloaded.
- **Freight Audit, rebuilt.** Shipments are found by their MBL and HBL numbers (the internal reference is shown small underneath), and both are searchable and in every export. Five tiles show shipments, invoices and a USD value: Delivered, Invoice Pending (estimated payable from the selected quote), Payment Pending, On Hold and Paid (invoice totals, freight plus additional charges). Also: quote versus invoice variance with an over-quote flag, aging of pending invoices and payments, payment terms with an overdue flag, a carrier summary, a monthly value chart, several invoices per shipment, On Hold (dispute) with a reason, a carrier invoice copy attachment, bulk Mark Paid and export, email reminders to carriers (queued in the demo outbox, no amounts), filters by period, carrier and mode, and settings for payment terms, tolerance and reminders. A new Freight Audit Register report is on the Reports page.
- **One shipment can hold several item types.** Set the type on each item line; the shipment shows as Mixed, and Shipments by Type has a Mixed group. Bulk upload no longer rejects rows of one shipment that have different types.
- **A blank PO number is no longer an error.** It is flagged PO Missing, listed in Data Quality and My Tasks, shown as a badge, and available as a PO Missing Only switch above the monitor.
- **Container types** are now 20GP, 20RF, 40GP, 40HC, 40RF and LCL (a dropdown on the entry form and in Edit Shipment). Old 20FT and 40FT values convert to 20GP and 40GP automatically. For reefer containers (20RF, 40RF) an optional set point (-40 to 40 C) can be entered; it can be left empty.
- Layout fixes: mode labels fit in the by-mode lists, no sideways scrolling on tablets, dates and units stay on one line, calendar buttons fit, wide tables show a shadow when more content is off-screen, and the Master file box starts as a small bar.
- **Shipment modes** are now Ocean, Ocean+Rail, Ocean+Truck, Air, Courier and Truck, each with its own icon. Existing Sea and Road shipments, saved data, backups and uploads are converted automatically (Sea becomes Ocean, Road becomes Truck). Container, free-time and CBM rules follow the mode: all three Ocean modes behave like ocean freight, Courier like Air for CBM, and Courier and Truck have no free-time tracking.
- The Reports page is laid out in groups with a featured Daily Status Report card and an icon for each report.
- **Reports page** (Insights): the Daily Status Report in your DSR template layout (34 columns), plus the shipment register, overdue milestones, shipments at risk, free time, delivery schedule, slot requests, data quality, carrier scorecard, Pending Invoices, Payment Pending, freight spend, RG Pending and the Monthly RG Accrual. Excel or CSV. The Daily Status Report lets you tick several years, quarters, months and statuses, choose whether the period follows the pickup date or the delivery date, and choose whether open shipments always show. Which role can download which report is set in Administration, Role Access, Report Access.
- **Freight Audit** (Commercial and Access): delivered shipments where your company pays the freight. Record actual freight cost, carrier invoice number and remarks; status Invoice Pending, Payment Pending or Paid.
- **RG Pending** (Operations, Logistics Analyst by default): DAP and DDP need only a Final RG after delivery; other terms need an In-Transit RG (with optional TO and PL#) once in transit, then a Final RG. Download the pending report, fill it in, upload it back.
- **Track & Trace access** is now editable per role (Role Access).
- Quick-filter switches above the monitor: Missing Docs only, Delayed only, Pending RG only.
- Account menu: Compact Table Rows, and Theme (match device, light or dark).
- Titles and subheadings use headline-style capitalisation.
- Optional shipping documents with a Missing Docs badge (run supabase-storage-setup.sql once for shared storage), and a Quotation ID on quotes.
- Sidebar sections open and close; profile, password, problem report and sign-out are in the avatar menu at the top right.
