# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: mini-project\todo.spec.js >> test
- Location: tests\mini-project\todo.spec.js:3:5

# Error details

```
Test timeout of 30000ms exceeded.
```

```
Error: locator.click: Test timeout of 30000ms exceeded.
Call log:
  - waiting for getByRole('link', { name: 'Active' })
    - locator resolved to <a class="" href="#/active">Active</a>
  - attempting click action
    - waiting for element to be visible, enabled and stable

```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
  - complementary [ref=e2]:
    - generic [ref=e3]:
      - heading "React" [level=3] [ref=e4]
      - generic [ref=e5]:
        - heading "React" [level=5] [ref=e6]
        - link "Source" [ref=e7]:
          - /url: https://github.com/tastejs/todomvc/tree/gh-pages/examples/react
        - heading "TypeScript + React" [level=5] [ref=e8]
        - link "Demo" [ref=e9]:
          - /url: https://todomvc.com/examples/typescript-react
        - text: ","
        - link "Source" [ref=e10]:
          - /url: https://github.com/tastejs/todomvc/tree/gh-pages/examples/typescript-react
    - separator [ref=e11]
    - blockquote [ref=e12]:
      - paragraph [ref=e13]: “ React is a JavaScript library for building user interfaces. You compose UI from function components and describe state with hooks; React handles the rendering and keeps the UI in sync as state changes. The modern ecosystem (createRoot, Suspense, Server Components) builds on the same component model. ”
      - link "React" [ref=e15]:
        - /url: http://facebook.github.io/react
    - separator [ref=e16]
    - heading "Official Resources" [level=4] [ref=e17]
    - list [ref=e18]:
      - listitem [ref=e19]:
        - link "Quick Start" [ref=e20]:
          - /url: https://react.dev/learn
      - listitem [ref=e21]:
        - link "API Reference" [ref=e22]:
          - /url: https://react.dev/reference/react
      - listitem [ref=e23]:
        - link "Philosophy" [ref=e24]:
          - /url: https://petehuntsposts.quora.com/React-Under-the-Hood
      - listitem [ref=e25]:
        - link "React Community" [ref=e26]:
          - /url: https://react.dev/community
    - heading "Community" [level=4] [ref=e27]
    - list [ref=e28]:
      - listitem [ref=e29]:
        - link "ReactJS on Stack Overflow" [ref=e30]:
          - /url: https://stackoverflow.com/questions/tagged/reactjs
    - generic [ref=e31]:
      - separator [ref=e32]
      - emphasis [ref=e33]:
        - text: If you have other helpful links to share, or find any of the links above no longer work, please
        - link "let us know" [ref=e34]:
          - /url: https://github.com/tastejs/todomvc/issues
        - text: .
  - generic [ref=e35]:
    - generic [ref=e36]:
      - heading "todos" [level=1] [ref=e37]
      - textbox "New Todo Input" [ref=e38]:
        - /placeholder: What needs to be done?
    - main [ref=e39]:
      - generic:
        - checkbox "❯ Toggle All Input" [checked] [ref=e40]
        - generic: ❯ Toggle All Input
      - list [ref=e41]:
        - listitem [ref=e42]:
          - generic [ref=e43]:
            - checkbox [checked] [ref=e44]
            - generic [ref=e45]: buy grocery
            - text: ×
        - listitem [ref=e46]:
          - generic [ref=e47]:
            - checkbox [checked] [ref=e48]
            - generic [ref=e49]: go for walk
            - text: ×
    - generic [ref=e50]:
      - generic [ref=e51]: 1 item left!
      - list [ref=e52]:
        - listitem [ref=e53]:
          - link "All" [ref=e54]:
            - /url: "#/"
        - listitem [ref=e55]:
          - link "Active" [ref=e56]:
            - /url: "#/active"
        - listitem [ref=e57]:
          - link "Completed" [ref=e58]:
            - /url: "#/completed"
      - button "Clear completed" [ref=e59] [cursor=pointer]
  - contentinfo [ref=e60]:
    - paragraph [ref=e61]: Double-click to edit a todo
    - paragraph [ref=e62]: Created by the TodoMVC Team
    - paragraph [ref=e63]:
      - text: Part of
      - link "TodoMVC" [ref=e64]:
        - /url: http://todomvc.com
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | 
  3  | test('test', async ({ page }) => {
  4  |   await page.goto('https://todomvc.com/examples/react/dist/');
  5  |   await page.getByTestId('text-input').click();
  6  |   await page.getByTestId('text-input').fill('buy grocery');
  7  |   await page.getByTestId('text-input').press('Enter');
  8  |   await page.getByTestId('text-input').fill('go to temple');
  9  |   await page.getByTestId('text-input').press('Enter');
  10 |   await page.getByTestId('text-input').fill('go for walk');
  11 |   await page.getByTestId('text-input').press('Enter');
  12 |   await page.getByRole('listitem').filter({ hasText: 'buy grocery' }).getByTestId('todo-item-toggle').check();
  13 |   await page.getByRole('listitem').filter({ hasText: 'go for walk' }).getByTestId('todo-item-toggle').check();
  14 |   await page.getByRole('link', { name: 'Completed' }).click();
  15 |   await page.getByRole('link', { name: 'Active' }).click();
  16 |   await page.getByRole('link', { name: 'Completed' }).click();
  17 |   await page.getByRole('link', { name: 'All' }).click();
> 18 |   await page.getByRole('link', { name: 'Active' }).click();
     |                                                    ^ Error: locator.click: Test timeout of 30000ms exceeded.
  19 |   await page.getByTestId('todo-item-label').click();
  20 |   await expect(page.getByTestId('todo-item-label')).toBeVisible();
  21 | });
```