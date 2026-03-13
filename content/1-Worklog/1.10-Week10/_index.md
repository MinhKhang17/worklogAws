---
title: "Week 10 Worklog"
date: 2026-03-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* **Backend**: Refine API endpoints — improve input validation, pagination, and write unit tests for core service methods.
* **Frontend**: Build the `ChatScreen` with AWS Bedrock AI integration and `ProfileScreen` with user account management.
* Deliver the AI-powered assistant feature as a differentiating value-add for the application.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Backend endpoint refinements <br>&emsp; + Add `@Valid` annotations and custom constraint validators to all request DTOs <br>&emsp; + Standardize paginated responses: `PageResponse<T>` with `page`, `size`, `totalPages`, `totalElements` <br>&emsp; + Add `GET /api/sessions/user/{userId}?startDate=&endDate=` date-range filter for session history | 03/17/2026 | 03/17/2026 | |
| 3   | - Write **unit tests** (Spring Boot Test + JUnit 5 + Mockito) <br>&emsp; + `UserWorkoutPlanServiceTest`: clone method, activate logic, IDOR prevention <br>&emsp; + `HealthCalculationServiceTest`: BMI/BMR/TDEE formulas for various inputs <br>&emsp; + `UserWorkoutSessionServiceTest`: active session query, deactivate behavior | 03/18/2026 | 03/18/2026 | |
| 4   | - Build **chatService** (Frontend) <br>&emsp; + Direct AWS Bedrock Runtime API call (no Lambda proxy) <br>&emsp; + Model: `anthropic.claude-3-5-haiku-20241022-v1:0` <br>&emsp; + Vietnamese system prompt: fitness coach persona <br>&emsp; + Send last 12 conversation turns as context (sliding window memory) | 03/19/2026 | 03/19/2026 | <https://docs.aws.amazon.com/bedrock/> |
| 5   | - Build **ChatScreen** (Frontend) <br>&emsp; + Full-screen chat UI with message bubble list (user / bot) <br>&emsp; + Animated "typing" indicator (3 bouncing dots) while waiting for response <br>&emsp; + 4 quick-option chips: "Suggest exercises", "Today’s menu", "Calorie goal", "Weight loss advice" <br>&emsp; + Vietnamese initial greeting from the fitness bot <br>&emsp; + Animated keyboard avoidance <br>&emsp; + `notifyAlert` error handling via global alert proxy | 03/20/2026 | 03/20/2026 | |
| 6   | - Build **ProfileScreen** (Frontend) <br>&emsp; + Display avatar (initial-letter fallback), name, email, username, birthdate, gender <br>&emsp; + Edit modal: update birthdate (YYYY-MM-DD) and gender via `updateUserProfile` API + `dispatch(updateUserProfile)` <br>&emsp; + Logout: `signOut` (Cognito revoke) + `dispatch(logout)` + clear secure storage <br>&emsp; + Delete account: `deleteUserProfile` + `signOut` — both gated by `ConfirmModal` | 03/21/2026 | 03/21/2026 | |

### Week 10 Achievements:

* **Backend — Refinements & Testing**:
  * All request DTOs now have `@Valid` constraints — invalid inputs return structured `ApiResponse` field errors.
  * `PageResponse<T>` standardizes all paginated endpoints consistently.
  * Date-range session filter (`?startDate=&endDate=`) working with `@DateTimeFormat` parsing.
  * Unit tests pass for `UserWorkoutPlanService` clone, activate, and IDOR prevention scenarios.
  * BMI/BMR/TDEE formulas verified with edge case inputs (min/max allowed ranges).
* **Frontend — AI Chat**:
  * `chatService.sendChatToBedrock` calls AWS Bedrock Runtime directly using credentials from `.env`.
  * Sliding window of 12 turns maintains conversation context economically.
  * Quick-option chips provide instant first interaction without typing.
  * Typing indicator creates natural chat feel; keyboard avoidance works on both iOS and Android.
* **Frontend — Profile**:
  * Profile data loaded from Redux `authSlice` — no extra API call needed on screen mount.
  * Edit modal updates local state optimistically and confirms via API.
  * Logout and delete account flows both require confirmation — no accidental data loss.

### AWS Knowledge Learned (Assumed Application):

* Learned the full container artifact flow: optimized Docker builds, immutable image tagging, and publishing backend images to Amazon ECR.
* Understood how ECS Fargate models deployment through task definitions, services, health checks, and desired task count.
* Studied container networking on AWS, including private subnets, outbound access through NAT, and ALB target group integration.
* Learned safe rollout patterns such as rolling updates and minimum healthy percent to reduce release risk.
* Practiced separating runtime configuration from the image itself through task-level environment variables and secret injection.
* Understood how GitHub Actions quality gates should protect AWS deployment stages by requiring lint, test, and build success first.
* Connected release observability with rollback decisions so deployment safety is based on measurable runtime behavior.

In summary, week 10 connected AWS container platform knowledge directly to a realistic deployment path for the backend.

### Next Week Plan:

* **Backend**: Final API review, Docker Compose refinement with health checks, environment variable documentation.
* **Frontend**: Build `HomeScreen` dashboard with parallel data fetching, resolve remaining bugs, and polish overall UX.
