# Fairway: cross-platform handicap tracker (iOS-first)

## What this is
A handicap tracking app for golfers, built iOS-first using Expo and React Native. The app calculates World Handicap System indexes transparently and surfaces deterministic, rules-based recommendations based on the user's scoring patterns. No AI, no LLM calls, no machine learning. Pure math and rules.

## Tech stack (do not deviate without asking first)
- Expo SDK 51+ with managed workflow
- React Native, TypeScript strict mode
- Expo Router for navigation (file-based)
- NativeWind v4 for styling (Tailwind for React Native)
- expo-sqlite for local persistence
- React Query (TanStack Query) for API state
- Zustand for client state
- Vitest for unit tests on pure logic
- Jest + React Native Testing Library for component tests
- RevenueCat for in-app subscriptions
- EAS Build and EAS Submit for iOS distribution

## Architecture
- Feature-based folder structure under /src
- /src/core/handicap is a pure TypeScript module with zero React or React Native imports. It only uses standard JS/TS.
- /src/features holds UI features (rounds, home, paywall, etc.)
- /src/services holds API clients and database wrappers
- /src/components holds shared UI primitives

## Code style
- TypeScript strict mode, no any unless justified in a comment
- Explicit return types on all exported functions
- Prefer pure functions where possible
- Functional components only, no class components
- Prettier defaults, ESLint with @typescript-eslint/strict

## Testing rules
- Every function in /src/core/handicap must have a unit test
- WHS calculations must be tested against published USGA worked examples, with the source URL cited inline in a test comment
- Run tests with: npm test
- Tests must pass before any PR is merged

## Workflow rules for Claude Code
- Open one PR per task, never bundle unrelated changes
- After any code change, run the relevant tests and report pass/fail in the PR description
- If a test fails, surface the failure rather than silently editing the test
- Conventional commit messages: feat:, fix:, test:, refactor:, chore:
- Never edit CLAUDE.md without explicit approval

## Important constraints
- No third-party UI kit (no NativeBase, no Tamagui, no React Native Paper). Build our own components on top of NativeWind.
- No AI, ML, or external LLM API calls anywhere in the codebase
- No analytics SDKs in v1 (we'll add posthog or similar later)
- Course data comes from golfcourseapi.com only. API key lives in .env, never committed.

## Domain notes
World Handicap System rules of handicapping are public:
https://www.usga.org/content/usga/home-page/handicapping/roh/Content/rules/Rules%20of%20Handicapping%20Home.htm

Key formulas the engine must implement correctly:
- Score Differential = (113 / Slope Rating) × (Adjusted Gross Score - Course Rating - PCC)
- Net Double Bogey cap = Par + 2 + handicap strokes received on that hole
- Handicap Index = average of lowest 8 of most recent 20 differentials
- Combined 9-hole scores per WHS 2024 update
- Exceptional Score Reduction when a differential is 7.0+ below current index
