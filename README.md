# NetCE Zendesk Guide Theme

The NetCE ZenDesk Guide theme is a customization of the default Zendesk Guide "Copenhagen" theme. It is designed to be responsive and accessible.
Learn more about customizing Zendesk Guide [here](https://support.zendesk.com/hc/en-us/sections/206670747).

This theme consists of a [set of templates](#templates), [styles](#styles), a Javascript file used mainly for interactions and an [assets folder](#assets).

## How to use
You can use command line tools or your favorite IDE to develop this theme, and preview your changes locally in a web browser using the Zendesk Apps Tools (ZAT). For details, see [Previewing theme changes locally](https://support.zendesk.com/hc/en-us/articles/115014810447).

### Manifest file
The manifest defines settings for this theme. You can read more about the manifest file [here](https://support.zendesk.com/hc/en-us/articles/115012547687).

#### Settings folder
If you have a variable of type 'file' in your manifest, you need to provide a default file for that variable in the `/settings` folder. This file will be used on the settings panel by default and users can upload a different file if they like.
Ex.
If you would like to have a variable for the background image of a section, the variable in your manifest file would look something like this:

```js
{
  ...
  "settings": [{
    "label": "Images",
    "variables": [{
      "identifier": "background_image",
      "type": "file",
      "description": "Background image for X section",
      "label": "Background image",
    }]
  }]
}

```
... and this would look for a file inside the settings folder named: `background_image` with any suitable extension.

## Publishing
This theme should be imported by ZenDesk directly from GitHub. Learn more [here](https://support.zendesk.com/hc/en-us/community/posts/360004400007).

**Do not import this theme using the Help Center web UI!**. Doing so will break GitHub integration and everybody will be very mad at you.

## Templates
The theme includes all the templates that are used for a Help Center that has *all* the features available. Not all of them are customized.

List of templates in the theme:
* Article page
* Category page
* Community post list page
* Community post page
* Community topic list page
* Community topic page
* Contributions page
* Document head
* Error page
* Footer
* Header
* Home page
* New community post page
* New request page
* Requests page
* Search results page
* Section page
* Subscriptions page
* User profile page

You can add up to 10 optional templates for:
 * Article page
 * Category page
 * Section page

You do this by creating files under the folders `templates/article_pages`, `templates/category_pages` or `templates/section_pages`.
Learn more [here](https://support.zendesk.com/hc/en-us/articles/360001948367).

## Styles
The styles that Theming Center needs to use in the theme are in the `style.css` file in the root folder.

The styles for the theme are split using Sass partials, all the partials are under [styles/](/blob/master/styles/), they are all included in the "main" file [index.scss](/blob/master/styles/index.scss) and then compiled to CSS.
If you wish to use SASS you can go to the [using SASS section](#using-sass)

## Assets
The NetCE theme doesn't have any assets at this time, but you can add assets to your theme by placing them in the `assets` folder.
You can add assets to the asset folder and use them in your CSS, Javascript and templates.
You can read more about assets [here](https://support.zendesk.com/hc/en-us/articles/115012399428)

# Using SASS
In order to use SASS for development, it is necessary to compile it into the CSS that Zendesk Guide understands. Zendesk App Tools [theme preview](#publishing-your-theme) currently *does not* support live SASS compilation.

## Requirements

- Install Ruby, we use `sassc` gem to compile our `.scss` files. You can see how to install Ruby [here](https://www.ruby-lang.org/en/documentation/installation/).
- Install `sassc` gem. You can run:
```
    gem install sassc
```

Now you can compile your SASS files running:
```
./bin/compile.rb
```
Which will take all the `scss` files inside the `styles/` folder and create the `style.css` file that is consumable by Zendesk Guide.

# Contributing
We use [conventional commits](https://conventionalcommits.org/) to improve readability of the project history and to automate the release process. The commit message should therefore respect the following format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

```

- type: describes the category of the change. See [supported types](#commit-types).
- scope: (optional) describes what is affected by the change
- description: a small description of the change
- body: (optional) additional contextual information about the change
- footer: (optional) adds external links, issue references and other meta-information

i.e.:

```
chore: automate release
fix(styles): fix button padding
feat(script): add auto focus to fields with errors
```

We use [`husky`](https://github.com/typicode/husky) and [`commitlint`](https://github.com/conventional-changelog/commitlint) to validate messages when commiting.

We use [Github actions](https://github.com/features/actions) together with [`semantic-release`](https://github.com/semantic-release/semantic-release) to release a new version of the theme once a PR gets merged. On each merge, `semantic-release` analyses the commit messages and infers a semantic version bump. It then creates a git tag, updates the manifest version and generates the corresponding [changelog](CHANGELOG.md).

## Commit types

The list bellow describes the supported commit types and their effect in the release and changelog.

| Type     | Description                                                                                            | Release | Changelog                |
|----------|--------------------------------------------------------------------------------------------------------|---------|--------------------------|
| build    | Changes that affect the build system or external dependencies                                          | -       | -                        |
| chore    | Other changes that don't modify the source code                                                        | -       | -                        |
| ci       | Changes to our CI configuration files and scripts                                                      | -       | -                        |
| docs     | Documentation only changes                                                                             | -       | -                        |
| feat     | A new feature                                                                                          | minor   | Features                 |
| fix      | A bug fix                                                                                              | patch   | Bug Fixes                |
| perf     | A code change that improves performance                                                                | patch   | Performance Improvements |
| refactor | A code change that neither fixes a bug nor adds a feature                                              | -       | -                        |
| revert   | Reverts a previous commit                                                                              | patch   | Reverts                  |
| style    | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) | -       | -                        |
| test     | Adding missing tests or correcting existing tests                                                      | -       | -                        |

## Breaking changes

Commits that add a breaking change should include `BREAKING CHANGE` in the body or footer of the commit message.

i.e.:

```
feat: update theme to use theming api v2

BREAKING CHANGE: theme is now relying on functionality that is exclusive to the theming api v2
```

This will then generate a major release and add a `BREAKING CHANGES` section in the [changelog](CHANGELOG.md).

# Bug reports
Bug reports must be submitted through NetCE's JIRA in the Customer Contact project: https://ceresource.atlassian.net/browse/CUST
