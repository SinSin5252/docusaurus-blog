# Docusaurus Blog Setup

This Docusaurus blog was created using a template and customized to fit my blog project.

## Table of Content

- [Customizing](#customizing)
    - [Main Page](#main_page)
    - [Navigation Bar](#navigation_bar)
    - [Footer](#footer)
- [Deployment](#deployment)


##  Customizing 

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/spmse/dev-blog-template"
    title="Github Tip" 
    type="tip"
>
Checkout this repository to see the code/implementation
</GithubLinkAdmonition>

### Main Page

This section changes the title and the tagline

```jsx title="/docusaurus.config.ts""
const config: Config = {
  title: "Sinan's DevSecOps Study Journal",
  tagline: 'Sinan Saglam - DevSecOps Enthusiast with a passion for details and efficiency',
  ...
}
```

The `editUrl` ist the parameter which contains the link to the Git repository. The placeholder can be defined in a .env file, which has to be pointed in the funktion `dotenvconfig()`. For orientation see [example.env](../../example.env)

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
.env file and set it `true`

```jsx title="/.env"
 BLOG_ENABLED=true
```


### Footer

For this project the Community colum in the footer was removed. To reduce the amount of the colums in the footer, the index of `.links[i].` changed to 1.

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

After reducing the index this section of the configuration has to be removed.

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

