# Benchmark Data

Pre-recorded response comparisons across 4 standard tasks. Token counts verified with tiktoken `cl100k_base` encoder.

> **Key distinction**: *Output token reduction* is the headline number (how much shorter responses are). *Estimated total session reduction* accounts for input tokens (which don't change), giving the honest real-world savings.

---

## Task 1: Web Search

**Prompt**: "Search for the latest Node.js LTS version"

### Normal Response (82 tokens)
```
I'll search for the latest Node.js LTS version for you.

Based on my search, the latest Node.js LTS version is Node.js 22.x (codename "Jod").
It entered LTS status in October 2024 and will be maintained until April 2027.
The current LTS release is v22.14.0.

Would you like me to help you install or upgrade to this version?
```

### Caveman Response (26 tokens)
```
Node.js 22.x LTS ("Jod"), current v22.14.0. Maintained until April 2027.
```

| Output Tokens | Reduction | Est. Session Savings |
|--------------|-----------|---------------------|
| 82 → 26 | 68% | 14-27% |

---

## Task 2: Code Edit

**Prompt**: "Add input validation to this function" (given a simple `createUser(name, email)` function)

### Normal Response (192 tokens)
```
I'll add input validation to the createUser function. Here's what I'm adding:
- Name validation: checking it's a non-empty string
- Email validation: checking it matches a basic email pattern
- Type checking for both parameters

Here's the updated function:

function createUser(name, email) {
  if (!name || typeof name !== 'string') {
    throw new Error('Name is required and must be a string');
  }
  if (!email || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    throw new Error('A valid email is required');
  }
  return { name: name.trim(), email: email.toLowerCase() };
}

I've added validation for both the name and email parameters. The name must be a
non-empty string, and the email must match a basic email format pattern. Let me know
if you'd like me to add any additional validation!
```

### Caveman Response (96 tokens)
```
Added name and email validation:

function createUser(name, email) {
  if (!name || typeof name !== 'string') {
    throw new Error('Name is required and must be a string');
  }
  if (!email || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
    throw new Error('A valid email is required');
  }
  return { name: name.trim(), email: email.toLowerCase() };
}
```

| Output Tokens | Reduction | Est. Session Savings |
|--------------|-----------|---------------------|
| 192 → 96 | 50% | 10-20% |

---

## Task 3: File Exploration

**Prompt**: "Find all TypeScript test files"

### Normal Response (148 tokens)
```
I'll search for all TypeScript test files in your project. Let me look through
the codebase for files matching common test patterns.

I found the following TypeScript test files:

- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts
- src/__tests__/utils.test.ts
- src/components/__tests__/Button.test.tsx
- src/components/__tests__/Modal.test.tsx
- e2e/login.spec.ts
- e2e/checkout.spec.ts

That's 7 test files total — 5 unit tests in src/__tests__/ and src/components/__tests__/,
plus 2 end-to-end tests in e2e/. Would you like me to look at any of these?
```

### Caveman Response (71 tokens)
```
Found 7 test files:
- src/__tests__/auth.test.ts
- src/__tests__/api.test.ts
- src/__tests__/utils.test.ts
- src/components/__tests__/Button.test.tsx
- src/components/__tests__/Modal.test.tsx
- e2e/login.spec.ts
- e2e/checkout.spec.ts
```

| Output Tokens | Reduction | Est. Session Savings |
|--------------|-----------|---------------------|
| 148 → 71 | 52% | 10-21% |

---

## Task 4: Q&A

**Prompt**: "Explain what this error means: `TypeError: Cannot read properties of undefined (reading 'map')`"

### Normal Response (209 tokens)
```
This error means you're trying to call the .map() method on a value that is undefined.
This is one of the most common JavaScript errors, and it typically happens when:

1. **Data hasn't loaded yet**: You're trying to map over an array that comes from an
   API call or async operation, but it hasn't been fetched yet.
2. **Wrong property path**: You're accessing a nested object property that doesn't
   exist (e.g., `response.data.items.map(...)` but `response.data.items` is undefined).
3. **Missing default value**: A function parameter or state variable wasn't initialized
   with a default array value.

**Common fixes:**
- Add optional chaining: `data?.map(...)`
- Provide a default: `(data || []).map(...)`
- Add a guard: `if (data) { data.map(...) }`
- Initialize state with an empty array: `useState([])`

Would you like me to help find where this is happening in your code?
```

### Caveman Response (58 tokens)
```
Calling `.map()` on `undefined` — something expected to be an array isn't set yet.

Fixes:
- `data?.map(...)` — optional chaining
- `(data || []).map(...)` — default to empty array
- `useState([])` — initialize state as array
```

| Output Tokens | Reduction | Est. Session Savings |
|--------------|-----------|---------------------|
| 209 → 58 | 72% | 14-29% |

---

## Summary

| Task | Normal Tokens | Caveman Tokens | Output Reduction |
|------|--------------|----------------|-----------------|
| Web Search | 82 | 26 | 68% |
| Code Edit | 192 | 96 | 50% |
| File Exploration | 148 | 71 | 52% |
| Q&A | 209 | 58 | 72% |
| **Average** | **158** | **63** | **61%** |

**Estimated total session savings**: 12-24% (accounting for input tokens, which typically make up 60-80% of total session tokens).

Sessions with many short Q&A exchanges see higher savings. Sessions dominated by large code generation see lower savings (the code itself doesn't shrink — only the wrapper around it does).
