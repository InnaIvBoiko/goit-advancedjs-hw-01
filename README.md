# Topic 2. Code Modularity — Homework

This is the homework project for **Topic 2: Code Modularity**. It contains two
tasks: a dynamically generated image gallery and a feedback form that persists
its state in local storage.

The project is built with [Vite](https://vitejs.dev/).

## Learning outcomes

By this point you already:

- understand what makes the JSON format special;
- know and use the methods of the `JSON` object;
- can tell web storage from local storage apart;
- have installed Node.js and use NPM (the Node package manager);
- understand the concept of code modularity;
- use the ECMAScript Modules syntax;
- know how to install and remove packages and use them in your code.

## Tasks

### Task 1. Image gallery

Implemented in `src/1-gallery.html` and `src/js/1-gallery.js`.

Build an image gallery with the [SimpleLightbox](https://simplelightbox.com/)
library, which fully handles clicks on images, opening and closing the modal
window, and navigating between images with the keyboard.

Key points:

- You no longer need to set up event delegation manually — SimpleLightbox tracks
  clicks on the gallery cards automatically. There is no need to add event
  listeners for gallery elements.
- A separate library for modal windows is not needed — opening the modal is
  built into SimpleLightbox.
- Libraries are installed via npm in the terminal, not through CDN links in
  `index.html`.

Gallery card markup template:

```html
<li class="gallery-item">
    <a class="gallery-link" href="large-image.jpg">
        <img
            class="gallery-image"
            src="small-image.jpg"
            alt="Image description"
        />
    </a>
</li>
```

Add SimpleLightbox as a project dependency with npm. To include the library's
CSS, add an extra import on top of the one described in the documentation:

```js
// Described in the documentation
import SimpleLightbox from 'simplelightbox';
// Additional styles import
import 'simplelightbox/dist/simple-lightbox.min.css';
```

Initialize the library **after** creating and appending the gallery elements to
`ul.gallery`. Then, using the **Options** section of the documentation, add
captions for the images taken from the `alt` attribute. The caption must be
positioned at the bottom and appear 250 ms after the modal window opens.

Acceptance criteria:

- The live page displays a gallery built from the `images` data array.
- The gallery is styled according to the layout.
- The gallery data is created dynamically in JS.
- There are no custom event listeners.
- SimpleLightbox is connected via npm.
- The library instance is initialized after the gallery elements are added to
  the DOM and outside of any function.
- Clicking a gallery element opens the library's modal window with the enlarged
  version of the clicked image, and all basic library functionality works.
- 250 ms after the modal opens, the `alt` attribute content appears at the
  bottom as the image caption.

### Task 2. Feedback form

Implemented in `src/2-form.html` and `src/js/2-form.js`.

Add the form markup to HTML and write a script that saves the field values to
local storage as the user types.

```html
<form class="feedback-form" autocomplete="off">
    <label>
        Email
        <input type="email" name="email" autofocus />
    </label>
    <label>
        Message
        <textarea name="message" rows="8"></textarea>
    </label>
    <button type="submit">Submit</button>
</form>
```

Requirements:

- Declare a `formData` object outside of any function, with `email` and
  `message` fields that start as empty strings: `{ email: "", message: "" }`.
- Use event delegation to track changes in the form via the `input` event. Save
  the current `email` and `message` values to `formData` and write that object
  to local storage under the `"feedback-form-state"` key.
- On page load, check whether there is data in local storage. If so, use it to
  populate both the form and the `formData` object. If not, leave the form
  fields empty.
- Before the form is submitted, make sure both fields are filled in. If any
  field (property of `formData`) is empty, show an alert with the text
  `Fill please all fields`. If all fields are filled, log the `formData` object
  with its current values to the console, then clear local storage, the
  `formData` object, and the form fields.

Acceptance criteria:

- The live page displays a form with two form elements and a submit button.
- The form is styled according to the layout.
- The form listens for the `input` and `submit` events.
- Typing into any form element writes the data to local storage under the
  `"feedback-form-state"` key, and the saved data has no leading or trailing
  whitespace.
- Entering data in one field does not erase the stored data of the other.
- On page reload the data from local storage is restored into the form fields,
  with no `undefined` values.
- On submit there is a check that both form elements are filled in.
- On submit, if both elements are filled, the object with `email`, `message` and
  their current values is logged to the console, and the storage and form fields
  are cleared.
- After a submit, typing into any form element does not bring back data from the
  previous submit.

## Project structure

```
src/
├── index.html        # home page with navigation
├── 1-gallery.html    # Task 1 — gallery markup
├── 2-form.html       # Task 2 — form markup
├── css/              # stylesheets
├── img/              # images
├── public/           # static assets copied as-is
└── js/
    ├── 1-gallery.js  # Task 1 logic
    └── 2-form.js     # Task 2 logic
```

HTML pages are linked from `index.html`:

```html
<ul>
    <li><a href="./1-gallery.html">Gallery</a></li>
    <li><a href="./2-form.html">Form</a></li>
</ul>
```

## Getting started

1. Make sure the LTS version of Node.js is installed on your computer.
   [Download and install](https://nodejs.org/en/) it if needed.
2. Install the project dependencies in the terminal with `npm install`.
3. Start development mode by running `npm run dev` in the terminal.
4. Open [http://localhost:5173](http://localhost:5173) in the browser. The page
   reloads automatically whenever you save changes to the project files.

Before submitting the homework, make sure the code is formatted with Prettier
(`npm run format`) and that there are no errors or warnings in the console when
the live page opens.

## Files and folders

- Page component markup files go in `src/partials` and are imported into
  `index.html`. For example, create the header markup `header.html` in the
  `partials` folder and import it into `index.html`.
- Stylesheet files go in `src/css` and are imported into the page HTML files.
  For example, the stylesheet for `index.html` is named `index.css`.
- Add images to `src/img`. The bundler optimizes them, but only when building
  the production version of the project. This happens in the cloud so it does
  not load your computer, since on weaker machines it could take a long time.

## Deployment

The production version of the project is automatically built and deployed to
GitHub Pages, into the `gh-pages` branch, every time the `main` branch is
updated — for example, after a direct push or a merged pull request. For this to
work, in `package.json` set the `--base=/<REPO>/` flag of the `build` command,
replacing `<REPO>` with your repository name, and push the changes to GitHub.

```json
"build": "vite build --base=/<REPO>/",
```

Then open the GitHub repository settings (`Settings` > `Pages`) and set the
production files to be served from the `/root` folder of the `gh-pages` branch,
if this was not done automatically.

### Deployment status

The deployment status of the latest commit is shown by an icon next to its
identifier.

- **Yellow** — the project is being built and deployed.
- **Green** — the deployment finished successfully.
- **Red** — an error occurred during linting, building, or deploying.

For more details, click the icon and follow the `Details` link in the popup.

### Live page

After a while, usually a few minutes, the live page becomes available at the
address shown on the `Settings` > `Pages` tab in the repository settings.

If a blank page opens, make sure there are no errors related to incorrect paths
to the project's CSS and JS files (**404**) in the `Console` tab. Most likely
the value of the `--base` flag of the `build` command in `package.json` is
incorrect.

## How it works

1. After every push to the `main` branch of the GitHub repository, a special
   script (GitHub Action) from the `.github/workflows/deploy.yml` file runs.
2. All repository files are copied to a server, where the project is initialized
   and goes through linting and building before deployment.
3. If all steps pass, the built production version of the project files is
   pushed to the `gh-pages` branch. Otherwise, the script's execution log will
   indicate the problem. </content> </invoke>
