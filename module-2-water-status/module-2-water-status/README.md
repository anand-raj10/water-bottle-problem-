# Module 2 – Water Point Status

Part of **P16 – The Empty Bottle Problem: Campus Drinking Water Management** (Next.js, React, MongoDB).

Students report the live condition of a campus water point: availability, cleanliness, temperature, working condition and usage/crowd status. Every report is saved in a history collection, and the water point itself is updated with the newest status, so Module 1 (Discovery) always shows fresh information and Module 3 (Maintenance) can pick up problem reports.

## Features
- Report form with 5 dropdowns and an optional description (max 300 characters)
- Validation on the client and again on the server (same `validateReport` function)
- Rule: a water point reported **Not Working** must also be **Not Available**
- Report history (newest first, max 50) and latest status of every water point
- Saving a report also updates the `WaterPoint` record (`lastReportedAt`, `usageStatus`, etc.)

## Folder structure
```
src/
 ├── app/
 │    ├── api/
 │    │    └── status-reports/
 │    │         └── route.js          # GET history, POST new report
 │    └── report/
 │         └── page.js                # route: /report
 │
 ├── models/
 │    └── WaterStatusReport.js        # report history schema
 │
 └── modules/
      └── water-status/
           ├── StatusReportPage.js    # page container
           ├── ReportForm.js          # report form
           ├── ReportHistory.js       # history list
           ├── LatestStatusList.js    # latest status per water point
           ├── UsageBadge.js          # crowd/usage badge
           ├── statusOptions.js       # dropdown values
           ├── validateReport.js      # validation rules
           └── status.css             # module styling
```

## API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/status-reports` | Latest reports (optional `?waterPointId=WP-001`) |
| POST | `/api/status-reports` | Validate, save a report and update the water point |

## Depends on the main project
This module is not standalone. Copy the folders into the main project (merge into `src/`). It uses these shared files from the full project:
- `src/lib/mongodb.js` – database connection
- `src/models/WaterPoint.js` – shared water point model
- `src/components/shared/StatusBadge.js` – status badge
- `jsconfig.json` – the `@/` import alias

## Run
1. `npm install`
2. Add `MONGODB_URI=mongodb://127.0.0.1:27017/campus_water` to `.env.local`
3. `npm run dev`, open `http://localhost:3000/api/seed` once, then `http://localhost:3000/report`

## Tech
Next.js (App Router), React, JavaScript, CSS, MongoDB + Mongoose.
