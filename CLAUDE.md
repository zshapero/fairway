Initialize an Expo + React Native + TypeScript project at the root of this repository.

Requirements:
- Use the Expo blank TypeScript template (npx create-expo-app with --template blank-typescript), but install it directly into the existing repository root, not into a subfolder. Preserve the existing CLAUDE.md and .git directory.
- Set up Expo Router with file-based routing under /app
- Install and configure NativeWind v4 for Tailwind-style styling, including tailwind.config.js, babel.config.js, and global.css
- Install dependencies: expo-sqlite, @tanstack/react-query, zustand
- Install dev dependencies: vitest, @testing-library/react-native, jest, @types/jest, eslint, prettier, @typescript-eslint/eslint-plugin
- Create a /src directory with subfolders: core/handicap, features, services, components, types
- Create a barebones /app/index.tsx that displays "Fairway" centered on screen using NativeWind classes
- Create a .env.example file listing the env vars we'll need (EXPO_PUBLIC_GOLF_COURSE_API_KEY)
- Add a comprehensive .gitignore (node_modules, .env, .expo, dist, ios, android)
- Set TypeScript to strict mode in tsconfig.json
- Add npm scripts: "start", "ios", "test", "lint", "typecheck"
- Open a single PR titled "chore: scaffold Expo project with TypeScript and NativeWind"

Acceptance criteria:
- npm install runs cleanly
- npm run typecheck passes with zero errors
- npm run lint passes with zero errors
- npm start launches the Expo dev server
- The PR description includes step-by-step instructions for me to test on my iPhone via Expo Go
