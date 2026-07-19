# Resume Creator Umbrella repo
A full-stack resume builder. Enables users to create, save, update and delete professional resumes. 

The project is split across three repositories:

### [Front end](https://github.com/axlothecook/Create_Resume)
The React app that represents the website's UI. Built as a single-page application.

### [Back end](https://github.com/axlothecook/Create_Resume-backend)
The Express API with MongoDB as the database. Controls account creation and login (cookie-based sessions) and the saved resumes.

### [Deploy](https://github.com/axlothecook/create-resume-deploy)
The config files that instruct how to deploy the project on my Raspberry Pi via a [CI/CD pipeline](https://github.com/axlothecook/homelab-ci-cd).

## How it fits together
The graph below shows how the repos connect at runtime. The Cloudflare Tunnel sends visitors to the frontend container, where nginx serves the static app and also proxies /api requests to the backend, so everything lives on one domain. The backend stores accounts and resumes in MongoDB; resumes are saved as JSON, so no file storage is needed. The backend and the database have no public address.

![image](https://github.com/user-attachments/assets/043bd02c-c83a-495e-82d8-0d4af87d2185)

## Deployment
The project is deployed via my [CI/CD pipeline](https://github.com/axlothecook/homelab-ci-cd): a push to the frontend or the backend runs that repo's tests, builds the arm64 image, and the Pi pulls it and restarts the stack. If any test fails, nothing gets deployed.

## Features
<ul>
  <li>build a resume section by section, with a live preview</li>
  <li>decide the order in which sections appear on the cv by dragging them up and down</li>
  <li>customise the layout, colours and fonts</li>
  <li>download the resume as a vector PDF</li>
  <li>with an account save up to 5 resumes and reload them later</li>
  <li>or browse as a guest: build and download without an account, but nothing gets saved</li>
  <li>has a light and dark mode switch</li>
  <li>fully responsive, with a dedicated mobile pass across every page</li>
</ul>

## Tech stack
Front end: [React 19](https://react.dev), [Vite](https://vite.dev), [@react-pdf/renderer](https://react-pdf.org) (vector PDF), [@dnd-kit](https://dndkit.com) (drag to reorder), plain CSS, [Vitest](https://vitest.dev) <br />
Back end: [Node.js](https://nodejs.org), [Express 5](https://expressjs.com), [MongoDB](https://www.mongodb.com) with [Mongoose](https://mongoosejs.com), [Passport](https://www.passportjs.org) sessions, [Jest](https://jestjs.io) <br />
Deploy: [Docker Compose](https://docs.docker.com/compose/), [GitHub Actions](https://github.com/features/actions) (GHCR, arm64), [Tailscale](https://tailscale.com) (CI to Pi), [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-tunnel/)
