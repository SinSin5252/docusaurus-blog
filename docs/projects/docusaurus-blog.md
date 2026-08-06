# Docusaurus Blog Setup

This website is built using this [template](https://github.com/Developer-Akademie-DevSecOpsKurs/dev-blog-template) and customized to fit my blog project.

## Table of Contents

  - [Quickstart](#quickstart)
    - [Prerequisites](#prerequisites)
  - [Usage](#usage)
    - [Repository Structure](#repository-structure)
    - [Main Page](#main-page)
    - [Navigation Bar](#navigation-bar)
    - [Footer](#footer)

## Quickstart

### Prerequisites

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/spmse/dev-blog-template"
    title="Template Info" 
    type="info"
>
Checkout this repository to see the code/implementation
</GithubLinkAdmonition>

- [Node.js](https://nodejs.org/) (v16 or later recommended)

navigate to your working directory

1. Clone Git Repository
```bash
git clone https://github.com/spmse/dev-blog-template.git
```

2. Installation

   ```
   npm install
   ```

3. Local Development

   ```
   npm start
   ```

   This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server. You can also open your local site with `localhost:3000` on your browser if it won't open automaticly.

##  Usage

### Repository Structure

The repository is organized as follows:

- `blog/`: Contains markdown files for blog posts. Blog-related metadata is automatically picked up by the Docusaurus configuration.
- `docs/`: Contains markdown files for documentation. These files are referenced in `sidebars.ts` to define the sidebar structure.
- `src/`: Contains custom React components, CSS, and JavaScript for additional functionality or theming.
- `static/`: Stores static assets (e.g., images, icons) served directly without processing.
- `sidebars.ts`: Configures the structure of sidebars in the documentation section.
- `docusaurus.config.ts`: Main configuration file for customizing and managing Docusaurus behavior.
- `build/`: Generated after running the `npm build` command. Contains the static website files ready for deployment.

New content can be added as follows:

- Add new documentation files to the `docs/` folder.
- Add new blog posts to the `blog/` folder. No additional configuration is required.

### Main Page

This section changes the title and the tagline

```jsx title="/docusaurus.config.ts"
const config: Config = {
  title: "Sinan's DevSecOps Study Journal",
  tagline: 'Sinan Saglam - DevSecOps Enthusiast with a passion for details and efficiency',
  ...
}
```

The `editUrl` is the parameter which contains the link to the Git repository. The placeholder can be defined in a `.env` file, which has to be pointed in the funktion `dotenvconfig()` in `docusaurus.config.ts` . For orientation see [example.env](../../example.env)

```jsx title="/docusaurus.config.ts"
editUrl:
            process.env.GIT_REPOSITORY_URL,

```

### Navigation Bar

This section defines the title and the logo on the top left corner with the items. The items can be placed left or right and can defined as a weblink or as a connection to the sidebar content.

```jsx title="/docusaurus.config.ts"
themeConfig: {
    // Replace with your project's social card
    image: 'img/docusaurus-social-card.jpg',
    navbar: {
      title: 'My Study Site',
      logo: {
        alt: 'My Site Logo',
        src: 'img/perrylogo.svg',
      },
      items: [
        {
          type: 'docSidebar',
          sidebarId: 'tutorialSidebar',
          position: 'left',
          label: 'Docs',
        },
        {
          href: process.env.GIT_REPOSITORY_URL,
          label: 'Github',
          position: 'right',
        },
      ],
    },
}
```
To enable the Blog button on the navigation bar, the `BLOG_ENABLED` value has to be added to the
`.env` file and set it `true`

```jsx title="/.env"
 BLOG_ENABLED=true
```

### Footer

For this project the "Community" colum is removed from the footer. To reduce the amount of the colums, the index of `.links[i].` set to 1.

```jsx title="/docusaurus.config.ts"
if (blogEnabled) {
  (config.themeConfig.navbar as any).items.push({to: '/blog', label: 'Blog', position: 'left'});
  (
    config.themeConfig.footer as any
  ).links[1].items.push({
    to: '/blog',
    label: 'Blog',
  });
}
```
 This section of the configuration has to be removed after changing the index.

```jsx title="/docusaurus.config.ts"
{
          title: 'Community',
          items: [
            {
              label: 'Stack Overflow',
              href: 'https://stackoverflow.com/questions/tagged/docusaurus',
            },
            {
              label: 'Discord',
              href: 'https://discordapp.com/invite/docusaurus',
            },
            {
              label: 'Twitter',
              href: 'https://twitter.com/docusaurus',
            },
          ],
        },
```