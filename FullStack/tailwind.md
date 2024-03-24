# TailwindCSS

## Tailwind CSS Intro / Basics

Tailwind is a utility framework using classes to easily build websites within html.

VS Code Extensions:

- Live Server (click ‘gear’ in settings) – search “Full reload” – check the box “By Default Liver Server inject CSS changes…”
  - Then in Terminal, type: `npx tailwindcss init`. This will create a tailwind.config.js file.
- Add extension:
  - `Tailwind CSS IntelliSense`
  - `Inline Fold` _(extension hides html classes – so that you only see/work with classes when you click on them)_

Create 2 directories:

- File: build
  - Index.html
    - (use the ! to create your html initial file)
- File: src
  - Input.css
    - @tailwind base;
    - @tailwind components;
    - @tailwind utilities;

Tailwind.config.js – file add to content:

- Content: ` [‘./’build/*.html’]`,

In VS Code:

- File menu > Preferences > Settings
  - Search unknown
  - Change from `‘warning’` to `‘ignore’` for tailwind

Terminal again:

- Run: ` npm tailwindcss -I ./src/input.css -o ./build/css/style.css`
  - This will create a `style.css` file under css folder within build

Index.html:

- Add Link under <head> just above </head>
  - `<link rel=”stylesheet” href=”css/style.css”>`
- Add after </head> .. body
  - `<div class=”bg-emerald-500 w-52 h-52”></div>`

Compile css – terminal:

- Run: `npx tailwindcss -I ./src/input.css -o ./build/css/style.css –watch`

**_Open with live server … Go Live from bottom R of VSC_**

Add classes to div:

- `<body class=”min-h-screen grid place-content-center”>`
  - `<div class=”bg-emerald-500 w-52 h-52 rounded-full shadow-2x1 grid place-content-center”>
    - `<div class=”bg-teal-200 w-32 h-32 rounded-full grid place-conetne-center”></div>`
  - </div>`

#### Misc. Helpful Hints:

- Check version of node by typing: `node -v` in your terminal.
- Ctrl B = hides file tree in VSC
- Use Tailwindcss.com website to search settings (i.e.: min-height)
