# Docusaurus Blog Setup

This Docusaurus blog was created using a template and customized to fit my blog project.

## TOC

- [Customizing](#customizing)
    - [Main Site](#main_site)
    - [Navigation Bar](#navigation_bar)
    - [Footer](#footer)


##  Customizing 

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/spmse/dev-blog-template"
    title="Github Tip" 
    type="tip"
>
Checkout this repository to see the code/implementation
</GithubLinkAdmonition>

### Main Site
```jsx title="/docusaurus.config.ts""
const config: Config = {
  title: "Sinan's DevSecOps Study Journal",
  tagline: 'Sinan Saglam - DevSecOps Enthusiast with a passion for details and efficiency',
  ...
}
```

```jsx title="/docusaurus.config.ts"
 url: process.env.DEPLOYMENT_URL ?? "https://SinSin5252.github.io",
  // Set the /<baseUrl>/ pathname under which your site is served
  // For GitHub pages deployment, it is often '/<projectName>/'
  baseUrl: process.env.BASE_URL ?? "/",

```


```jsx title="/docusaurus.config.ts"
 url: process.env.DEPLOYMENT_URL ?? "https://SinSin5252.github.io",
  // Set the /<baseUrl>/ pathname under which your site is served
  // For GitHub pages deployment, it is often '/<projectName>/'
  baseUrl: process.env.BASE_URL ?? "/",

```

```jsx title="/docusaurus.config.ts"
editUrl:
            process.env.GIT_REPOSITORY_URL,
```
### Navigation Bar
```jsx title="/docusaurus.config.ts"
themeConfig: {
    // Replace with your project's social card
    image: 'img/docusaurus-social-card.jpg',
    navbar: {
      title: 'My Study Site',
      logo: {
        alt: 'My Site Logo',
        src: 'img/perrylogo.svg',
        ...
      }
    }
}
```
### Footer

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

## Description

## Further References