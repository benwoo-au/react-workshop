# Tests

There's no code to run with `npm start`. Show the tests and run `npm test` if you want to show them pass/fail

# Main Topics to Cover

- ✅ Using Vitest with React Testing Library
- ✅ Testing Approaches - Test the way the user interacts with the UI
- ✅ Mocking

Also review:
https://kentcdodds.com/blog/common-mistakes-with-react-testing-library

## How to install on your own project

Since this app already uses Vite, Vitest is the natural fit. It reuses your existing Vite config (aliases, plugins, etc.).

```sh
npm install --save-dev vitest happy-dom @testing-library/react @testing-library/jest-dom
```

In `vite.config.ts`

```ts
/// <reference types="vitest/config" />

export default defineConfig({
  // ... your existing config
  test: {
    environment: 'happy-dom',
    globals: true,
    setupFiles: ['./src/test/setup.ts'],
    include: ['**/test.tsx', '**/*.{test,spec}.{js,mjs,cjs,ts,mts,cts,jsx,tsx}'],
  },
})
```

Create `src/test/setup.ts`

```ts
import '@testing-library/jest-dom/vitest'
```

In `package.json`

```json
"scripts": {
  "test": "vitest run",
  "test:watch": "vitest"
}
```

## TypeScript Tests

Vitest ships with its own types. Add this to your app `tsconfig`:

```json
"compilerOptions": {
  "types": ["vitest/globals"]
}
```

With `globals: true`, you can use `describe`, `it`, `expect`, and `vi` without importing them. Import `vi` when you want to be explicit in examples, like `vi.fn()` and `vi.mock()`.

## Jest → Vitest cheat sheet

| Jest | Vitest |
| --- | --- |
| `jest.fn()` | `vi.fn()` |
| `jest.mock()` | `vi.mock()` |
| `jest.requireActual()` | `vi.importActual()` |
| `jest.Mock` | `Mock` from `'vitest'` |
| `testEnvironment: 'jsdom'` | `environment: 'happy-dom'` |
