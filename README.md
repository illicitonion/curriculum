# Curriculum Platform

## What is it?

This is a white label multi-tenant platform for us and our code school friends to use to manage our curricula. It's built on top of [Hugo](https://gohugo.io/) and [Netlify CMS](https://www.netlifycms.org/).

The platform, layout, styles and components are all developed in the Hugo module [/common-theme](/common-theme).

The content is developed in the Hugo module [/common-content](/common-content). This content is all headless blocks. It doesn't create any pages on your site unless you call it somewhere.

Multi-language support is provided by [Hugo's i18n support](https://gohugo.io/content-management/multilingual/).

Each org builds its own Hugo site that uses the common theme and content modules, and then makes any customisations they need and deploys it wherever they want.

## Examples

- [CodeYourFuture](/org-cyf/) => [https://org-cyf-theme.netlify.app/](https://org-cyf-theme.netlify.app/)
- [MigraCode](/org-mcb/) => [https://org-mcb-theme.netlify.app/](https://org-mcb-theme.netlify.app/) (couldn't find an svg logo)

## To build a new site

1. In the root of this repo, run:

```bash
hugo new site org-<your-org-name>
cd org-<your-org-name>
```

2. Initialise your new site as a hugo module, as only modules can import modules:

```zsh
hugo mod init github.com/CodeYourFuture/curriculum-labs/org-<your-org-name>
```

Then add the common theme and content modules as hugo modules to hugo.toml:

```toml
[module]
  [[module.imports]]
    path = "github.com/CodeYourFuture/curriculum-labs/common-theme"
  [[module.imports]]
    path = "github.com/CodeYourFuture/curriculum-labs/common-content"
    [[module.imports.mounts]]
      source = "en"
      target = "content"
```

Look at the [org-cyf](/org-cyf/) and [org-mcb](/org-mcb/) examples for more details and options.

To customise the css, make a dir `assets/custom-theme` and throw any scss in there. It will be compiled and added last.

To add site logo/s, make a dir and add svgs to `assets/custom-images/site-logo/`. They will be added to the site header.

Add your content to `content/` and customise the site config in `config.toml`. Please contribute any improvements you make back to the common theme and content modules.

## To locally develop your site

Having to commit and push to github to see your changes is a pain. To develop your site locally, you can assign replace directives to your hugo modules in `go.mod`:

```go
// go.mod
replace github.com/CodeYourFuture/curriculum-labs/common-theme => /Users/YOU/PATH_TO/LOCAL/curriculum-labs/common-theme

replace github.com/CodeYourFuture/curriculum-labs/common-content => /Users/YOU/PATH_TO/LOCAL/curriculum-labs/common-content
```

Then run `hugo server` as normal.

Note, you should be able to do this in with env, and it looks like really for this setup we should have production and development config files, but I hit my limit of twiddling with hugo config and gave up. If you know how to do this, please sort it out.
