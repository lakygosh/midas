# Personal Finance Tracker – Product Requirements Document (PRD)

## 1. Introduction / Overview
The Personal Finance Tracker is a cross-platform (Android & iOS) mobile application built with Flutter. It enables power users to record day-to-day expenses, schedule recurring costs, log incomes, and track investments—all in multiple currencies—and instantly visualise their financial health through an analytics dashboard. The primary objective is to provide an extremely **fast, friction-less input flow** and **clear, actionable insights**, so the user can customise the product to their needs today and extend it with automations tomorrow (with an eye toward monetisation).

## 2. Goals
1. Allow a user to add a transaction (expense, income, investment) in < 15 s.
2. Provide real-time analytics for the current month and historical data for at least the past 12 months.
3. Support multiple currencies with on-the-fly conversion to a user-selected base currency.
4. Operate offline and **auto-sync** data when a connection is available.
5. Enable account sharing between multiple users in the same household **from day 1**.
6. Lay technical foundations to add future automations (e.g., bank import) without breaking changes.

## 3. User Stories
1. **As a power user**, I want to add a one-off expense quickly so that my records stay accurate even when I'm on the move.
2. **As a power user**, I want to define a recurring monthly cost (e.g., rent) so that it is logged automatically each cycle.
3. **As a power user**, I want to input my monthly income, savings contributions, and investment purchases so that I see a complete picture of cash flow.
4. **As a household member**, I want to share an account with my partner so that we both see and manage the same budget.
5. **As a user**, I want to view dashboards (pie, bar, line charts) that summarise spending by category and trends over time so that I can spot areas to optimise.

## 4. Functional Requirements
1. The system **shall** let the user create a one-off expense with fields: amount, currency, date (default today), category, optional note.
2. The system **shall** let the user create a recurring expense with a frequency (daily / weekly / monthly / yearly) and an optional end date.
3. The system **shall** let the user log income entries with fields: amount, currency, date, category, optional note.
4. The system **shall** let the user log investment transactions with fields: amount, currency, asset type (text), date, optional note.
5. The system **shall** support CRUD (create, read, update, delete) on all transaction types.
6. The system **shall** support multiple currencies, storing both original currency and a converted value to the user's base currency (using daily FX rates).
7. The system **shall** categorise expenses and incomes; default category list is provided, and the user can add/edit categories.
8. The system **shall** provide a dashboard with:
   a. Bar chart: income vs. expenses per month (12 months)
   b. Pie chart: current-month expenses by category
   c. Line chart: net worth trend across months (income – expenses + investments)
   d. Table: Top 5 expense categories (current month)
9. The system **shall** show analytics updates in real time after each transaction is saved (local calculation, then server sync).
10. The system **shall** work entirely offline with local persistence (SQLite); once online, it **shall** sync with the ASP .NET Core API.
11. The backend **shall** expose REST/GraphQL endpoints secured with JWT for CRUD operations and user management.
12. The system **shall** support multi-user accounts: owner can invite members via email; members have equal permissions except deleting the account.
13. The system **shall** provide basic export to CSV for all transactions of a selected period.

## 5. Non-Goals (Out of Scope for MVP)
• Automatic bank statement import (Open Banking).  
• Crypto-exchange integrations.  
• AI-based categorisation.  
• Web or desktop client.  
• In-app purchases / subscription monetisation.

## 6. Design Considerations
• Adopt **Material Design 3** components provided by Flutter.  
• Dark & light themes based on system settings.  
• Use intuitive FAB (+) for adding a transaction; minimise steps to completion.  
• Dashboard charts use contrasting colours, accessible colour palette (WCAG AA).

## 7. Technical Considerations
• **Frontend:** Flutter 3.x, state management with Riverpod or Bloc.  
• **Backend:** ASP .NET Core 8 Web API, Entity Framework Core with MySQL.  
• **Database schema:** Transactions, Categories, Users, Accounts, RecurringRules, FXRates.  
• **Sync:** Timestamp-based conflict resolution (last-write-wins) for offline edits.  
• **Deployment:** Self-hosted on user's Ubuntu server (Docker container). APK side-loaded on devices.  
• **Testing:** Unit tests for business logic, integration tests for API endpoints.

## 8. Success Metrics
• Median time-to-create-transaction ≤ 15 s (measured via analytics).  
• ≥ 95 % sync success within 5 s after connectivity is restored.  
• Dashboard renders < 500 ms for 10 k transactions on a mid-range device.  
• ≤ 1 % crash rate in production (Firebase Crashlytics).  
• 80 % of beta users report that insights are "clear" or "very clear" in user survey.

## 9. Open Questions
1. Do we need receipt photo attachments in MVP?  
2. Which FX rate provider (e.g., ECB API) will be used, and how frequently updated?  
3. What is the exact sharing model—single shared ledger per household or multiple ledgers?  
4. Do we need role-based permissions (viewer vs. editor) for shared accounts?  
5. Which charting library in Flutter (e.g., fl_chart vs. charts_flutter) will we adopt? 