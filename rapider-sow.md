<!-- Rapider Official App SOW & Specification | App #177: Personal Task & To-Do Management (personal-task-and-to-do-management) | Domain: PRS -->

# #177 Personal Task & To-Do Management (`personal-task-and-to-do-management`) — Scope of Work (SOW)

- **App Number & Name:** `#177` — Personal Task & To-Do Management
- **Proposed App Key:** `personal-task-and-to-do-management`
- **Suite / Domain Key & Model Prefix:** `PER` (`Prs*` — `PrsTask*` family)
- **Representative Product (`P1`):** Todoist
- **Combined Feature Catalog:** [../combined-features/177-personal-task-and-to-do-management-features.md](../combined-features/177-personal-task-and-to-do-management-features.md)
- **Target Release Posture:** Owner-Isolated Personal GTD Vault, Natural-Language Capture, Mindful Daily Time-Blocking, Eisenhower Matrix, Pomodoro Focus & Habit Consistency Microapplication

---

## 1. Executive Outcome & Target Audience

### 1.1 Consumer & Knowledge-Worker Problem Solved
Individuals juggle household errands, bills, appointments, learning goals, side projects, and work assignments across sticky notes, chat self-DMs, and rigid corporate project trackers—leading either to dropped commitments or overwhelming, guilt-inducing overdue backlogs. Worse, putting personal errands inside corporate project tools (`apm`) exposes private life details to employers and managers. **Rapider Personal Task & To-Do Management (`personal-task-and-to-do-management`)** provides a **strictly owner-isolated (`ownerUserRef == authenticatedActor`)** GTD and daily time-blocking sanctuary that pairs instant natural-language capture with realistic daily capacity planning, Pomodoro focus execution, and non-punitive habit tracking.

### 1.2 Fast-Path Everyday Flow vs. Power-User GTD Depth
- **Fast-Path Everyday Defaults (Zero-Config Users, Students, Families):** Open straight into **My Day** and **Inbox**, type `"Call dentist tomorrow 10am p1"` in Quick Add, check off items in one click, and share a single *Groceries* list with a partner—no folders, tags, or rituals required.
- **Progressive Power-User Depth (GTD Practitioners, Freelancers, Busy Executives):** Unlock **Areas of Responsibility**, *When Date* vs. *Hard Deadline* separation (*Today* / *This Evening* / *Someday*), `<rapider-kanban>` boards, 4-quadrant **Eisenhower Matrix**, 15-minute visual time-blocking with read-only `ApmIssue` work-task pull, Pomodoro timers, guided morning/shutdown rituals, and consent-scoped AI task breakdown.

### 1.3 Measurable Outcomes
- **Sub-4-Second Task Capture:** Deterministic inline NLP parses dates, recurrence, durations, `#list`, `@label`, and `p1`–`p4` without opening modal pickers.
- **>= 35% Reduction in Chronic Overdue Rollover:** Separating *When* (`scheduledDate`) from *Hard Deadline* (`deadlineDate`) plus a daily capacity bar (e.g., `5.5h / 6.0h`) curates realistic daily slates.
- **100% Personal Privacy Guarantee:** Server-enforced owner isolation guarantees `0` unauthorized reads of personal tasks, habits, or reflections by workspace or employer administrators.

### 1.4 Benchmark Summary (`P1`–`P6`)
Synthesizes the natural-language speed, time-blocking calendar, and Capture/Ramble AI of **`P1` Todoist**, the integrated Eisenhower Matrix, Pomodoro timer, and Habit tracker of **`P2` TickTick**, the calm *When-vs-Deadline* and *This Evening* GTD craft of **`P3` Things 3**, the mindful daily rituals, capacity guardrails, and one-way work-task pull of **`P4` Sunsama**, the auto-resetting *My Day* smart slate of **`P5` Microsoft To Do**, and the clean personal-vs-enterprise boundary of **`P6` Zoho ToDo**.

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### 2.1 In-Scope Capabilities
1. Owner-isolated personal task vault (`PrsTaskItem`, `PrsTaskList`, `PrsTaskSection`) with Inbox, Life Areas, Sections, Checklists, `P1`–`P4` priorities, `@labels`, and saved smart filters (`PrsTaskSavedFilter`).
2. Deterministic client + server natural-language Quick Add parser supporting fixed (`FIXED_SCHEDULE`) and completion-relative (`AFTER_COMPLETION`) recurrence rules.
3. Auto-resetting **My Day** daily slate (*Morning / Afternoon / This Evening*), guided Morning Plan & Evening Shutdown rituals (`PrsTaskDailyRitual`), and visual 15/30-minute time-blocking with capacity bars.
4. Interactive `<rapider-kanban>` board view, 4-quadrant **Eisenhower Matrix**, pause-aware **Pomodoro / Stopwatch Focus Timer** (`PrsTaskFocusSession`), and daily/weekly **Habit Tracker** (`PrsTaskHabit`, `PrsTaskHabitCheckIn`).
5. Opt-in one-way read-only **Assigned at Work** panel referencing the user's own `ApmIssue` and Home `WorkItem` assignments for personal time-boxing without leaking private tasks back to `APM`.
6. Explicit per-list household/partner sharing (`PrsTaskShareGrant`), CSV/JSON/ICS portability, masked external ICS feed tokens, and review-before-apply grounded AI task breakdown & brain-dump extraction.

### 2.2 Out-of-Scope Capabilities (Delegated to Adjacent Rapider Apps)
- **Team Agile sprints, story points, epics, burndown charts, and corporate issue workflows:** Owned by `apm` (`ApmProject`, `ApmSprint`, `ApmIssue`) and `#040` Project & Portfolio Management.
- **Billable client timesheets, utilization rates, and payroll/invoice billing:** Owned by `time` (`ApmTimesheet`) and `billing` (`FinInvoice`).
- **Long-form rich knowledge bases, wikis, and multi-page notebooks:** Owned by Rapider Platform Notebooks and `#048` Wiki & Team Knowledge Base.
- **Deep biometric recovery, multi-set gym load tracking, and GPX endurance logs:** Owned by `#181 Personal Health & Fitness Tracking` (`PerFit*` / `PerWel*`).

### 2.3 Suite Ownership & Integration Contract Matrix

| Domain / App | Owns | Integration Contract with `personal-task-and-to-do-management` |
| :--- | :--- | :--- |
| **`PER` (`personal-task-and-to-do-management`)** | `PrsTaskList`, `PrsTaskSection`, `PrsTaskItem`, `PrsTaskSavedFilter`, `PrsTaskDailyRitual`, `PrsTaskFocusSession`, `PrsTaskHabit`, `PrsTaskHabitCheckIn`, `PrsTaskShareGrant` | Primary owner of private/household tasks, daily rituals, Pomodoro focus logs, and personal micro-habits under `ownerUserRef`. |
| **`APM` (`apm`)** | `ApmProject`, `ApmSprint`, `ApmIssue` | Strictly **one-way read-only** lookup of `ApmIssue`s where `assigneeUserRef == authenticatedActor` so the user can reserve personal focus blocks; private `PrsTaskItem`s NEVER sync into `APM`. |
| **Platform Home `WorkItem`s** | Cross-app actionable notifications & approvals | Receives shared-list invitations (`PrsTaskShareGrant`) and async import review notices; user's assigned `WorkItem`s can optionally appear in the read-only *Assigned at Work* sidebar. |
| **Platform Calendar & Files** | Shared Calendar busy/free overlays & malware-scanned file blobs | Reads user's Calendar busy blocks for time-blocking; publishes optional masked `"Personal Focus Block"` slots; stores task attachments and JSON/CSV/ICS export archives in private Platform Files. |
| **Platform Channels & AI** | ACL-scoped `projectChannelMessage` & LLM gateway | Hosts shared-list item discussion threads and owner-private AI Daily Coach / Ramble extraction previews. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture (13 Pages)

Every visible sidebar section strictly enforces the **Minimum 3 Visible Items Rule (`>= 3`)** (`Overview`: 3 items, `Lists & Views`: 3 items, `Focus & Governance`: 3 items = 9 visible items; 4 detail/drawer views hidden from sidebar).

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `my-day` | **My Day & Rituals** | `Overview` | `true` (Order 1) | Auto-resetting daily slate (*Morning / Afternoon / This Evening*), NLP Quick Add bar, capacity progress bar (`plannedMinutes` vs. daily cap), Morning/Shutdown ritual drawer trigger, and optional collapsible *Assigned at Work* side tray. |
| 2 | `inbox-tasks` | **Inbox & All Tasks** | `Overview` | `true` (Order 2) | Bulk `findSWR` master GTD Inbox and filterable task table/list, `#activeFilterTagsBar` with `[Clear all]`, instant client-side search, clickable task title -> `task-detail`, icon+text `Edit`, and icon-only `Delete`. |
| 3 | `upcoming-calendar` | **Upcoming & Time-Blocking** | `Overview` | `true` (Order 3) | Day / 7-Day / Month visual timeline grid with 15/30m drag-and-drop task time-blocking alongside read-only Calendar events and hard-deadline banners. |
| 4 | `areas-and-lists` | **Areas & Personal Lists** | `Lists & Views` | `true` (Order 1) | Life Areas (*Personal*, *Home*, *Finance*, *Learning*), personal & household shared `PrsTaskList` cards, progress rings, reusable checklist templates, and list/board toggle using `<rapider-kanban>`. |
| 5 | `priority-matrix` | **Eisenhower & Kanban** | `Lists & Views` | `true` (Order 2) | Switchable 4-quadrant Eisenhower Matrix and `<rapider-kanban>` board (by Priority, Section, or Day Bucket) with `#activeFilterTagsBar` and saved smart filter pills (`PrsTaskSavedFilter`). |
| 6 | `habits` | **Daily Habits** | `Lists & Views` | `true` (Order 3) | Weekly habit check-in grid (`COMPLETED`, `SKIPPED`, `null` unlogged), flexible grace-goal streaks (`e.g., 5x/wk`), and quick habit creation drawer. |
| 7 | `focus-timer` | **Pomodoro Focus Studio** | `Focus & Governance` | `true` (Order 1) | Distraction-free Pomodoro (`25/5`, `50/10`) & stopwatch runner bound to active `PrsTaskItem`, pause-aware elapsed timer, subtask checklist tick-off, and session history table. |
| 8 | `logbook-insights` | **Logbook & Insights** | `Focus & Governance` | `true` (Order 2) | Searchable completed `PrsTaskItem` Logbook, weekly focus hours by Life Area, planned-vs-actual estimation accuracy chart, and ritual consistency summary across light/dark themes. |
| 9 | `privacy-sharing` | **Sharing, Portability & Privacy** | `Focus & Governance` | `true` (Order 3) | Active `PrsTaskShareGrant` household list permissions, revocable masked ICS calendar token, Todoist/TickTick CSV/JSON import, full data export, and cryptographic cascade delete. |
| 10 | `task-detail` | **Task Detail & Subtasks** | *(Hidden)* | `false` | Full task workspace (`#/task-detail?id=...`) with *When* vs. *Deadline* dates, recurrence inspector, nested checklist steps, Platform File attachments, AI *"Make Actionable"* preview, `projectChannelMessage` notes, and `Back to list` state restoration. |
| 11 | `list-detail` | **Personal List Workspace** | *(Hidden)* | `false` | Single `PrsTaskList` view (`#/list-detail?id=...`) with custom `PrsTaskSection` headings, `<rapider-kanban>` toggle, household share drawer trigger, and `#activeFilterTagsBar`. |
| 12 | `new-task-drawer` | **Quick / Full Task & Brain-Dump Drawer** | *(Hidden)* | `false` | Sliding creation/edit drawer supporting single-task structured entry + AI Ramble/Screenshot batch extraction staging table; auto-closes via `closePageDrawer()` with `finally` button reset. |
| 13 | `share-list-drawer` | **Share Personal List Drawer** | *(Hidden)* | `false` | Sliding drawer to grant or revoke `VIEWER`/`EDITOR` access on a single `PrsTaskList` (optional SMS/phone invite lookup via `<rapider-phone-input>` or user email) and dispatch a Home `WorkItem`. |

**Rapider UI Standards Enforced Across All 13 Pages:**
- Initial data loads exclusively invoke `window.rapiderApi.findSWR` and `countSWR` with clean filters (zero manual `isDeleted` where-clauses in network payloads) plus defensive client-side `items = rawData.filter(item => item && item.isDeleted !== true)`.
- Active search/filter conditions render `#activeFilterTagsBar` (`Active:`, HTML-escaped `Search: "..." ✕` / `Priority: "..." ✕` chips, and `[Clear all]`).
- Table `Actions` columns NEVER include a `View` button; clicking the primary `title` navigates to `task-detail` or `list-detail`; `Edit` is icon + text (`<i class="fas fa-edit mr-1"></i><span>Edit</span>`); `Delete` is icon-only (`title="Delete" aria-label="Delete"`) confirmed via `#rapiderConfirmOkBtn` with zero native `alert`/`confirm`/`prompt`.
- All primary and destructive buttons enforce `#ffffff !important` text contrast in both light and dark modes.

---

## 4. Canonical Data Models (`PrsTask*` — 8 Models)

All models omit `projectId` (relying on platform context) and enforce server-resolved `ownerUserRef` isolation, platform UUIDs (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in deterministic seeds), and optimistic `version`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`PrsTaskList`** | `id` (UUID), `ownerUserRef` (UUID), `areaName` (String: `Personal`, `Home`, `Finance`, `Health`, `Learning`, `Side Project`), `name` (String), `colorHex` (String), `iconKey` (String), `isInbox` (Boolean), `isTemplate` (Boolean), `defaultView` (`LIST` \| `KANBAN`), `sortOrder` (Int), `version` (Int) | Has many `PrsTaskSection`, `PrsTaskItem`, `PrsTaskShareGrant` | Exactly one system-provisioned `isInbox = true` list per owner (cannot be deleted or shared); archiving a list preserves completed Logbook items. |
| **`PrsTaskSection`** | `id` (UUID), `ownerUserRef` (UUID), `listId` (UUID), `title` (String), `sortOrder` (Int), `isCollapsed` (Boolean), `version` (Int) | Belongs to `PrsTaskList`; groups `PrsTaskItem` | Deleting a section moves its open tasks to unsectioned list root rather than silently deleting user tasks. |
| **`PrsTaskItem`** | `id` (UUID), `ownerUserRef` (UUID), `listId` (UUID), `sectionId` (UUID?), `parentTaskId` (UUID?), `title` (String), `notesMarkdown` (String?), `status` (`TODO` \| `IN_PROGRESS` \| `WAITING` \| `DONE` \| `CANCELED`), `priority` (`P1_URGENT` \| `P2_HIGH` \| `P3_MEDIUM` \| `P4_LOW`), `eisenhowerQuadrant` (`DO_FIRST` \| `SCHEDULE` \| `DELEGATE` \| `ELIMINATE`?), `labels` (String[]), `dayBucket` (`MORNING` \| `AFTERNOON` \| `THIS_EVENING` \| `ANYTIME` \| `SOMEDAY`), `isCommittedMyDay` (Boolean), `myDayDate` (LocalDate?), `scheduledDate` (LocalDate?), `scheduledStartAt` (DateTime?), `plannedMinutes` (Int?), `deadlineDate` (LocalDate?), `recurrenceMode` (`NONE` \| `FIXED_SCHEDULE` \| `AFTER_COMPLETION`), `recurrenceRule` (String?), `timezoneId` (IANA String), `checklistSteps` (Embedded `{stepId, text, isDone}`[]), `completedAt` (DateTime?), `version` (Int) | Belongs to `PrsTaskList`; optional `linkedWorkEntityRef` (`ApmIssue` / `WorkItem` UUID, read-only), `attachmentFileRefs` (Platform Files[]), `channelThreadRef` (`projectChannelMessage`) | `scheduledDate` (*When*) may never overwrite `deadlineDate` (*Hard Due*); checking off a recurring task stamps immutable completion in Logbook and spawns/advances the next occurrence according to `recurrenceMode` in `timezoneId`. |
| **`PrsTaskSavedFilter`** | `id` (UUID), `ownerUserRef` (UUID), `name` (String), `filterSpecJson` (Object: priorities, labels, lists, maxMinutes, dueWindow), `isPinned` (Boolean), `sortOrder` (Int), `version` (Int) | Evaluates over owner's `PrsTaskItem`s | Saved filter expressions never widen ACL scope beyond `ownerUserRef` and active `PrsTaskShareGrant` lists. |
| **`PrsTaskDailyRitual`** | `id` (UUID), `ownerUserRef` (UUID), `ritualDate` (LocalDate), `dailyCapacityHours` (`Decimal128`, e.g., `6.00`), `plannedTotalHours` (`Decimal128`), `actualFocusedHours` (`Decimal128`), `topThreeTaskIds` (UUID[]), `morningPlannedAt` (DateTime?), `eveningShutdownAt` (DateTime?), `privateReflectionWin` (String?), `version` (Int) | References `PrsTaskItem`s for `ritualDate` | Unique `(ownerUserRef, ritualDate)` constraint; `privateReflectionWin` is strictly owner-only and excluded from shared lists and workspace admin APIs. |
| **`PrsTaskFocusSession`** | `id` (UUID), `ownerUserRef` (UUID), `taskId` (UUID?), `mode` (`POMODORO` \| `STOPWATCH`), `startedAt` (DateTime), `endedAt` (DateTime?), `pausedTotalSeconds` (Int), `actualFocusSeconds` (Int), `sessionStatus` (`RUNNING` \| `PAUSED` \| `COMPLETED` \| `DISCARDED`), `version` (Int) | Optional `taskId` -> `PrsTaskItem` | Only one `RUNNING` session per owner at a time; `actualFocusSeconds` excludes `pausedTotalSeconds`; `COMPLETED` sessions become immutable ledger entries. |
| **`PrsTaskHabit`** | `id` (UUID), `ownerUserRef` (UUID), `name` (String), `areaName` (String), `targetDaysPerWeek` (Int: `1..7`), `preferredDayBucket` (`MORNING` \| `AFTERNOON` \| `THIS_EVENING`), `currentStreakWeeks` (Int), `isArchived` (Boolean), `version` (Int) | Has many `PrsTaskHabitCheckIn` | `targetDaysPerWeek` supports grace days (e.g., `5` completions/week maintains weekly streak without punishing rest days). |
| **`PrsTaskHabitCheckIn`** | `id` (UUID), `ownerUserRef` (UUID), `habitId` (UUID), `localDate` (LocalDate), `state` (`COMPLETED` \| `SKIPPED`), `note` (String?), `version` (Int) | Belongs to `PrsTaskHabit` | Unlogged days remain absent (`null` in UI, never falsified as `SKIPPED` or `0`); unique `(ownerUserRef, habitId, localDate)`. |
| **`PrsTaskShareGrant`** | `id` (UUID), `ownerUserRef` (UUID), `listId` (UUID), `granteeUserRef` (UUID), `granteePhoneE164` (String?), `accessRole` (`VIEWER` \| `EDITOR`), `grantStatus` (`PENDING` \| `ACTIVE` \| `REVOKED`), `workItemRef` (UUID?), `revokedAt` (DateTime?), `version` (Int) | Belongs to `PrsTaskList` (`isInbox == false`); links to Platform Home `WorkItem` | Cannot grant on `isInbox = true`; revoking sets `grantStatus = REVOKED` and immediately terminates grantee query/command access (`403 Forbidden`). |

---

## 5. Core End-to-End User Journeys

### 5.1 Natural-Language Capture, Completion-Relative Recurrence & Click-Through Detail (`inbox-tasks` -> `task-detail` -> `inbox-tasks`)
1. On `#/inbox-tasks`, the user types `"Replace HVAC filter every! 90 days tomorrow 6pm for 20m #Home @maintenance p2"` into the Quick Add bar.
2. Live token chips preview `scheduledDate = Tomorrow`, `dayBucket = THIS_EVENING`, `plannedMinutes = 20`, `recurrenceMode = AFTER_COMPLETION (90d)`, `list = Home`, `labels = [@maintenance]`, `priority = P2_HIGH`. Pressing **Add** optimistically inserts the row and clears SWR cache.
3. Filtering by `@maintenance` displays `#activeFilterTagsBar` (`Label: "@maintenance" ✕ [Clear all]`). The user clicks the task title link, smoothly navigating to `#/task-detail?id=...` (verified free of `<base href>` path hijacking), adds two checklist steps (*Check size 16x25x1*, *Vacuum intake vent*), and clicks **Back to list**, restoring `#/inbox-tasks` with the `@maintenance` filter intact.
4. Checking off the task three days later calculates the next occurrence `90 days` from the actual completion date (not the original scheduled date) and records the finished instance in `logbook-insights`.

### 5.2 Mindful Morning Ritual, One-Way Work Bridge & Realistic Time-Blocking (`my-day` -> `upcoming-calendar`)
1. At `08:30`, the user opens `#/my-day` and clicks **Start Morning Plan**. The ritual drawer shows `3.5h` of meetings from Platform Calendar, `2` personal deadline items, and `1` assigned `ApmIssue` (`"Review Q4 API spec"`, read-only from `apm`) in the *Assigned at Work* tray.
2. The user drags `"Review Q4 API spec"` (`90m`) and three personal tasks (`"Pay utility bill" 15m`, `"Prep tax folder" 45m`, `"Grocery pickup" 30m` in *This Evening*) onto `#/upcoming-calendar`.
3. `PrsTaskDailyRitual` updates `plannedTotalHours = 3.00` against `dailyCapacityHours = 3.50` (`Decimal128`). Meanwhile, a manager viewing `apm` sees **zero** trace of `"Pay utility bill"` or `"Prep tax folder"`.

### 5.3 Pomodoro Focus Execution & Pause-Aware Effort Tracking (`focus-timer` -> `logbook-insights`)
1. From `#/my-day`, the user clicks **Focus** on `"Prep tax folder"`, opening `#/focus-timer` with a `25:00` Pomodoro timer.
2. Midway, the user pauses for `4m 10s` to answer the door, resumes, finishes the interval, ticks off subtasks, and marks the task `DONE`.
3. `PrsTaskFocusSession` persists `actualFocusSeconds = 1500` and `pausedTotalSeconds = 250` (`pausedTotalSeconds` strictly excluded from focused totals), immediately updating `#/logbook-insights`.

### 5.4 Household Shared List Invite & Instant Revocation (`areas-and-lists` -> `share-list-drawer` -> Home `WorkItem`)
1. On `#/areas-and-lists`, the user opens the *Family Groceries* list (`#/list-detail?id=...`) and clicks **Share List**, opening `share-list-drawer`.
2. Entering their partner's account (with optional E.164 lookup via `<rapider-phone-input>`) and `EDITOR` role creates a `PENDING` `PrsTaskShareGrant`, dispatches a Rapider Home `WorkItem` to the partner, and auto-closes the drawer via `closePageDrawer()`.
3. Once accepted, the partner can add/check off items in *Family Groceries* only—attempts to query the owner's `Inbox`, `PrsTaskHabit`, or `PrsTaskDailyRitual` return `403 Forbidden`. Revoking the grant on `#/privacy-sharing` immediately cuts off access to *Family Groceries* as well.

### 5.5 Consent-Scoped AI Brain-Dump ("Ramble") & Task Breakdown (`new-task-drawer` / `task-detail`)
1. Opening `new-task-drawer` in **Brain-Dump Mode**, the user pastes a messy paragraph: *"Need to renew passport before June 15, book passport photo this Saturday morning, and mail old passport next Tuesday"*.
2. The grounded AI extractor populates a 3-row editable staging table (`Renew passport` w/ `deadlineDate = June 15`; `Book passport photo` w/ `scheduledDate = Saturday MORNING`; `Mail old passport` w/ `scheduledDate = Tuesday`). Nothing is written to the database until the user reviews, edits a duration, and clicks **Create 3 Tasks**.

---

## 6. Consolidated Feature Priorities & Work Packages (`P0`, `P1`, `P2`)

### `P0` Foundation Work Packages
- **WP-P0-1 — Owner-Isolated Vault, NLP Quick Add & GTD Hierarchy (`PTD-001`–`PTD-006`):** Implement server-enforced `ownerUserRef` guard (`403` to workspace admins), `PrsTaskList`, `PrsTaskSection`, `PrsTaskItem`, `PrsTaskSavedFilter`, inline NLP parser, *When* vs. *Deadline* + *This Evening* semantics, `FIXED_SCHEDULE` / `AFTER_COMPLETION` recurrence, `inbox-tasks`, `areas-and-lists`, `task-detail`, `list-detail`, and `new-task-drawer`.
- **WP-P0-2 — My Day Slate, Kanban, Eisenhower Matrix & Time-Blocking (`PTD-008`–`PTD-010`, `PTD-014`):** Deliver auto-resetting `my-day`, `<rapider-kanban>` board, 4-quadrant `priority-matrix`, and 15/30-minute `upcoming-calendar` time-blocking with `Decimal128` capacity bar.
- **WP-P0-3 — Pomodoro Focus Timer & Data Portability (`PTD-015`, `PTD-020`):** Deliver pause-aware `PrsTaskFocusSession` on `focus-timer`, Todoist/TickTick CSV/JSON import, full JSON/CSV/ICS export, and cascade personal data erasure on `privacy-sharing`.

### `P1` Consumer Power & Household Scale Work Packages
- **WP-P1-1 — Guided Rituals, Work Bridge, Reminders & Templates (`PTD-007`, `PTD-011`–`PTD-013`, `PTD-018`):** Build `PrsTaskDailyRitual` morning/shutdown flows, one-way read-only `ApmIssue`/`WorkItem` personal time-boxing tray, multi-offset snoozable reminders, message/file task capture, and checklist templates.
- **WP-P1-2 — Daily Habits, Logbook Insights & Household List Sharing (`PTD-016`, `PTD-017`, `PTD-019`, `PTD-021`):** Build `PrsTaskHabit` + `PrsTaskHabitCheckIn` (`null` vs. `SKIPPED` honesty), `logbook-insights`, `PrsTaskShareGrant` household collaboration via Home `WorkItem`s (`share-list-drawer`), and revocable masked ICS feed tokens.

### `P2` Adjacent & Grounded AI Work Packages
- **WP-P2-1 — Consent-Scoped AI Breakdown, Ramble Extraction & Cross-Personal Links (`PTD-022`–`PTD-026`):** Deliver review-before-apply AI subtask breakdown, text/voice/screenshot brain-dump task extraction, overcommitment deferral coaching in private `projectChannelMessage` threads, NL-to-`#activeFilterTagsBar` chip translation, and intra-owner `PER` deep links (`#178`, `#180`, `#182`).

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Personal Owner** | Full CRUD on own `PrsTask*` records, Inbox, Life Areas, Habits, Focus Sessions, Daily Rituals, AI prompts, imports/exports, masked ICS tokens, and `PrsTaskShareGrant` issuance/revocation. | Read-only on linked work `ApmIssue`s within `#177` (must open `apm` to mutate work issue status if governed by project workflows). |
| **Shared List Collaborator (`EDITOR`)** | Read, create, check off, edit, and comment (`projectChannelMessage`) on `PrsTaskItem`s and `PrsTaskSection`s strictly inside the single explicitly granted `PrsTaskList` while `grantStatus == ACTIVE`. | **Zero access (`403`)** to the owner's `Inbox`, other `PrsTaskList`s, `PrsTaskDailyRitual` reflections, `PrsTaskHabit`s, `PrsTaskFocusSession`s, or `linkedWorkEntityRef` details; cannot delete the shared list or re-share it. |
| **Shared List Collaborator (`VIEWER`)** | Read-only view of `PrsTaskItem`s inside the single granted `PrsTaskList` while `grantStatus == ACTIVE`. | Cannot create, edit, check off, reorder, or delete tasks; zero access to any other owner records. |
| **Workspace / Employer Administrator** | Enable/disable the microapplication in workspace catalog and monitor aggregate anonymous service health (error rate, queue latency). | **STRICTLY BLOCKED (`403 Forbidden`)** from reading, listing, searching, auditing, or exporting any user's `PrsTask*` tasks, titles, notes, habits, focus sessions, or ritual reflections (`PTD-001`). |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### 8.1 Guarded Domain Commands
All commands resolve `ownerUserRef` from authenticated JWT claims (never from client payloads) and require `idempotencyKey`, `correlationId`, and `expectedVersion`:
- `per.task.quickCaptureAndParse` — Parses natural-language input deterministically (or commits structured drawer payload) into `PrsTaskItem` with timezone-validated dates.
- `per.task.completeTaskOccurrence` — Marks `PrsTaskItem` completed in Logbook and atomically calculates/spawns the next occurrence for `FIXED_SCHEDULE` or `AFTER_COMPLETION` rules.
- `per.task.commitDailyRitual` — Upserts `PrsTaskDailyRitual` (`MORNING_PLAN` or `EVENING_SHUTDOWN`), rolls over/defers selected tasks, and recomputes `Decimal128` `plannedTotalHours`.
- `per.task.completeFocusSession` — Finalizes `PrsTaskFocusSession` excluding `pausedTotalSeconds` and increments `PrsTaskDailyRitual.actualFocusedHours`.
- `per.task.grantOrRevokeListShare` — Issues `PrsTaskShareGrant` + recipient Home `WorkItem`, or atomically revokes collaborator access and invalidates cached tokens.
- `per.task.exportOrEraseVault` — Generates an encrypted user-private JSON/CSV/ICS bundle in Platform Files or executes irreversible cryptographic erasure of all `PrsTask*` records for `ownerUserRef`.

### 8.2 Domain Events Published & Consumed (Kafka)
- **Published:** `per.task.item.created.v1`, `per.task.item.completed.v1`, `per.task.focus.completed.v1`, `per.task.list.shareChanged.v1`, `per.task.vault.erased.v1` (payloads contain opaque IDs only—never task titles or personal notes on shared telemetry topics).
- **Consumed:** `apm.issue.assigned.v1` (updates optional read-only personal time-blocking cache if user enabled work bridge), `platform.file.malware_scan_completed.v1`.

### 8.3 `requiredWorkflows` (Declared in `app.manifest.json`)
1. `personalTaskRecurrenceAndMyDayResetWorkflow` — Performs timezone-aware midnight *My Day* resets per user IANA timezone without auto-mutating hard deadlines, and generates due reminders.
2. `personalTaskImportExportPortabilityWorkflow` — Processes Todoist/TickTick/Microsoft To Do CSV/JSON imports with deduplication staging and packages JSON/CSV/ICS personal exports.
3. `personalTaskAiBreakdownAndCaptureWorkflow` — Executes consent-scoped AI subtask decomposition and voice/screenshot task extraction into non-destructive preview staging payloads.
4. `personalTaskVaultErasureWorkflow` — Executes cascade deletion across `PrsTask*`, revokes ICS tokens, purges private attachments, and emits completion audit proof to the owner.

### 8.4 Grounded Rapider AI Rules
- AI features (`PTD-023`–`PTD-026`) operate **strictly within the authenticated user's consented `PrsTask*` scope**; private personal prompts and task contents are never used to train tenant/global models or exposed to workspace admins.
- AI breakdown, brain-dump extraction, and schedule re-balancing **never auto-mutate, delete, or reschedule tasks silently**—every suggestion renders an explicit preview diff requiring a human **Apply / Confirm** click.

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **Strict Personal Vault Isolation (GDPR / CCPA / Workplace Privacy):** Every database read, search index, SWR cache key, and attachment URL enforces `ownerUserRef == authenticatedActor` (or active `PrsTaskShareGrant` for a specific non-Inbox `listId`). Even if a user accesses Rapider via a corporate workspace SSO account (whether on a `\$0.00` free personal tier or `\$5.00`/month consumer pro tier), employer admins cannot inspect personal tasks.
- **Calendar Title Masking:** When publishing personal time-blocks to an external or workspace calendar feed (`PTD-021`), default privacy mode masks titles as `"Personal Focus Block"` unless the owner explicitly toggles full-title visibility.
- **Timezone & DST Integrity:** All *My Day* resets, habit check-ins (`LocalDate`), and recurring schedules store the user's explicit IANA `timezoneId` so travel or Daylight Saving Time shifts never drop or duplicate daily tasks.
- **Accessibility & Responsive UX:** Full WCAG 2.2 AA compliance (keyboard-first task check-off, ARIA labels on icon-only Delete buttons, `#ffffff !important` text contrast on primary/danger buttons across light and dark modes) and responsive layouts at `390px` mobile, `768px` tablet, and `1440px` desktop.

---

## 10. Deterministic Acceptance Criteria

1. **Owner-Only Privacy Enforcement (`403 Forbidden`):** An authenticated Workspace Administrator querying `findSWR('PrsTaskItem')`, `PrsTaskHabit`, or `PrsTaskDailyRitual` belonging to another user receives `0` records / `403 Forbidden` at the server layer.
2. **Sidebar 3-Item Section Rule:** `app.manifest.json` defines 3 visible sidebar sections (`Overview`, `Lists & Views`, `Focus & Governance`), each containing exactly 3 visible pages (`displayOnMenu: true`), while all 4 detail/drawer routes set `displayOnMenu: false`.
3. **SWR & Clean Query Compliance:** All initial page loads use `findSWR` / `countSWR` with zero redundant `isDeleted` API query filters and filter `item.isDeleted !== true` in memory.
4. **Deterministic NLP & Recurrence Semantics:** Entering `"Water plants every! 7 days tomorrow 8am #Home @chore p3"` creates a `PrsTaskItem` with `recurrenceMode = AFTER_COMPLETION`; completing it 2 days late schedules the next occurrence `7 days` after actual completion rather than 5 days later.
5. **When Date vs. Hard Deadline Separation:** Deferring `scheduledDate` (*When*) from *Today* to *This Evening* or *Next Week* leaves `deadlineDate` completely unchanged.
6. **Active Filter Tags & Clear All:** Entering a search term or clicking a Priority/Label pill on `inbox-tasks` or `priority-matrix` displays `#activeFilterTagsBar` with HTML-escaped dismissible chips and `[Clear all]`, synchronously updating both list rows and `<rapider-kanban>` cards; clicking `Clear all` restores all items.
7. **Table Action Standard & Custom Elements:** Data tables contain zero standalone "View" buttons in `Actions`; task/list names navigate to detail views, `Edit` renders icon + text, `Delete` renders icon-only (`title="Delete" aria-label="Delete"`), `priority-matrix` / `areas-and-lists` use `<rapider-kanban>`, and `share-list-drawer` uses `<rapider-phone-input>`.
8. **Optimistic Mutations & Drawer Lifecycle:** Checking off, editing, or deleting a task updates in-memory state immediately, clears SWR cache, uses `#rapiderConfirmOkBtn` (zero `window.alert`/`confirm`/`prompt`), and `new-task-drawer` / `share-list-drawer` reset buttons in `finally` and invoke `closePageDrawer()`.
9. **One-Way Work Bridge Leak Prevention:** Time-blocking an assigned `ApmIssue` inside `my-day` creates no `PrsTaskItem` exposure inside `apm`, and creating a private `PrsTaskItem` triggers zero writes or events visible to `apm` project boards.
10. **Pause-Aware Focus Timer Math:** Pausing a `25:00` Pomodoro session for `120` seconds records `pausedTotalSeconds = 120` excluded from `actualFocusSeconds`, and prevents two concurrent `RUNNING` sessions for the same owner.
11. **Honest Habit Null vs. Skipped Semantics:** Unlogged past days on `habits` render `Unavailable / Unlogged` (`null`) rather than `0` or `SKIPPED`, and meeting a `5x/week` target preserves the weekly streak.
12. **Scoped Household Share & Instant Revocation:** Sharing *Family Groceries* grants collaborator access strictly to that `listId` after Home `WorkItem` acceptance; revoking `PrsTaskShareGrant` immediately blocks subsequent reads and writes (`403`) on that list.
13. **Click-Through Navigation & Base-URL Guard:** Clicking a task title on `inbox-tasks` transitions cleanly to `#/task-detail?id=...` without `<base href>` 404 diversion, and clicking `Back to list` restores prior `#activeFilterTagsBar` chips.
14. **No `projectId` Leakage & Theme Contrast:** Zero `PrsTask*` schemas or mutation payloads include `projectId`, and all 13 pages pass `validate_theme` across light and dark modes with `#ffffff !important` primary/danger button text.
