## Relevant Files

- `backend/PersonalFinance.Api/Models/*.cs` – Entity Framework Core entity classes for each data model (User, Account, Category, Transaction, RecurringRule, FXRate).
- `backend/PersonalFinance.Api/Controllers/*.cs` – REST API controllers exposing CRUD and auth endpoints.
- `backend/PersonalFinance.Api/Services/CurrencyService.cs` – Service that fetches and caches FX rates.
- `backend/tests/` – Unit & integration tests for backend logic and controllers.
- `mobile/lib/main.dart` – Flutter entry point and app configuration.
- `mobile/lib/models/*.dart` – Domain models mirrored from backend.
- `mobile/lib/providers/*.dart` – Riverpod/Bloc providers for state management.
- `mobile/lib/screens/transaction/` – UI for listing, adding and editing transactions/investments.
- `mobile/lib/screens/category/` – UI to manage expense/income categories.
- `mobile/lib/screens/dashboard/dashboard_screen.dart` – Main dashboard with charts.
- `mobile/lib/services/api_service.dart` – HTTP client wrapper handling JWT and requests.
- `mobile/lib/services/sync_service.dart` – Offline-first synchronisation logic.
- `mobile/lib/widgets/charts/*.dart` – Re-usable chart widgets (bar, pie, line).
- `mobile/test/` – Widget/unit tests for Flutter code.

### Notes

- Unit tests should be located alongside the code they test (e.g., `TransactionForm.dart` and `TransactionForm.test.dart` in the same directory).
- Use `dotnet test` to run backend tests and `flutter test` to run mobile tests.

## Tasks

- [ ] 1.0 Project Setup & Core Architecture
  - [ ] 1.1 Initialise Git repository and create project folders (`mobile/`, `backend/`, `infra/`).
  - [ ] 1.2 Create Flutter project with null-safety; add dependencies: `flutter_riverpod`, `fl_chart`, `sqflite`, `intl`, `dio`.
  - [ ] 1.3 Create ASP .NET Core Web API project targeting .NET 8; add packages: `Pomelo.EntityFrameworkCore.MySql`, `Microsoft.AspNetCore.Authentication.JwtBearer`.
  - [ ] 1.4 Configure Docker Compose for API and MySQL containers.
  - [ ] 1.5 Define shared data models/ER diagram and document in `docs/data-model.md`.
  - [ ] 1.6 Add GitHub Actions workflow to build & test both mobile and backend projects.

- [ ] 2.0 Backend: Data Models & API Endpoints
  - [ ] 2.1 Implement EF Core entities and migrations for `Users`, `Accounts`, `Categories`, `Transactions`, `RecurringRules`, `FXRates`.
  - [ ] 2.2 Seed default categories and base currency per account.
  - [ ] 2.3 Create CRUD endpoints for Categories (`/api/categories`).
  - [ ] 2.4 Create CRUD endpoints for Transactions (expenses, income, investments) at `/api/transactions`.
  - [ ] 2.5 Implement service & scheduled job to evaluate recurring rules and generate instances.
  - [ ] 2.6 Implement `CurrencyService` that fetches daily FX rates and stores them in `FXRates` table.
  - [ ] 2.7 Implement authentication endpoints (`/auth/register`, `/auth/login`) with JWT issuance.
  - [ ] 2.8 Write unit & integration tests for services and controllers.

- [ ] 3.0 Frontend: Transaction & Category Management
  - [ ] 3.1 Define Dart models mirroring backend entities.
  - [ ] 3.2 Setup Riverpod providers (auth, transactions, categories).
  - [ ] 3.3 Build Transaction List screen with filtering by month and category.
  - [ ] 3.4 Build Add/Edit Transaction forms for expense, income, investment with currency input & validation.
  - [ ] 3.5 Build Category Management screen (list, add, edit, delete).
  - [ ] 3.6 Implement `ApiService` using Dio with JWT token handling.
  - [ ] 3.7 Write widget & unit tests for forms, providers, and API integration.

- [ ] 4.0 Offline Persistence & Sync
  - [ ] 4.1 Design local SQLite schema equivalent to backend models.
  - [ ] 4.2 Implement Data Access Layer using Drift (or raw `sqflite`).
  - [ ] 4.3 Implement `SyncService`: detect local changes, queue remote updates, pull remote changes, resolve conflicts (last-write-wins).
  - [ ] 4.4 Integrate background sync with `workmanager` (Android) / `background_fetch` (iOS).
  - [ ] 4.5 Write tests covering offline scenarios and conflict resolution.

- [ ] 5.0 Analytics Dashboard Implementation
  - [ ] 5.1 Implement analytics helpers to calculate monthly totals, category aggregates, and net-worth trend.
  - [ ] 5.2 Build chart widgets (bar, pie, line) using `fl_chart`.
  - [ ] 5.3 Create Dashboard screen displaying charts and Top 5 expense categories table.
  - [ ] 5.4 Connect Dashboard to Riverpod providers and ensure real-time updates on data change.
  - [ ] 5.5 Optimise performance (render < 500 ms for 10 k records) & write widget tests.

- [ ] 6.0 Multi-User Account Sharing & Authentication
  - [ ] 6.1 Backend: Implement invite endpoints (`/accounts/{id}/invite`) and email sending stub.
  - [ ] 6.2 Backend: Add middleware to enforce roles (owner vs. member).
  - [ ] 6.3 Frontend: Build Auth flow (login, register, token refresh, logout) with secure storage.
  - [ ] 6.4 Frontend: Build UI for managing account members and sending invites.
  - [ ] 6.5 Ensure sync logic supports multi-user edits and resolves conflicts.
  - [ ] 6.6 End-to-end tests covering shared account workflows. 