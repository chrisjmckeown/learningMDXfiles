---
title: "Storybook"
excerpt: "Learnings from Storybook, tips and tricks."
date: "2022-08-10"
source: ["https://storybook.js.org/", "https://tsdx.io/"]
author:
  name: Chris McKeown
tags: ["Storybook", "code"]
---

<h1 align="center">Storybook</h1>

---

# Storybook

[chrisjmckeown/storybook-my-component](https://github.com/chrisjmckeown/storybook-my-component)

- Create react app
- Then run npx sb init
- Make sure to add anything that you want to expose it is in the entry file, index.tsx

## Essential addons

### Docs

- Add comments above props and the component for them to show in the Docs section

### Controls

### Actions

- Add onClick etc. handlers

### Viewport

### Backgrounds

### Toolbars & globals

### Measure & outline

## Addins

### [storybook-addon-a11y](https://storybook.js.org/addons/@storybook/addon-a11y/)

- `npm i -D @storybook/addon-a11y`
- Go to the .storybook/main.js and add mdx to stories, i.e. `stories: ['../stories/**/*.stories.@(ts|tsx|js|jsx|mdx)'],`

## MDX

- Go to the .storybook/main.js and add `'@storybook/addon-a11y'` to the addins
- Add a new file i.e. `Button.stories.mdx`

# TSDX

[TSDX](https://tsdx.io/) is a zero-config CLI that helps you develop, test, and publish modern TypeScript packages with ease--so you can focus on your awesome new library and not waste another afternoon on the configuration.

- `npx tsdx create my-component` to create a project
- Note: first time it will ask to install `tsdx`
- Select the template, basic, react or react-with-storybook
- In one terminal run TSDX `npm start` to listen for changes to automatically build files
- In another terminal run Storybook `npm run storybook` which will run on localhost:6006
- Once complete:
  - run `npm run build`

# Deploying to NPM

[Build And Publish A React Component Library](https://www.youtube.com/watch?v=hf6Z8OZanec)

- to deploy privately to npm you need a paid account
-
