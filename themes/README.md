# Compose

Compose is a [Hugo](https://gohugo.io/) theme for documentation or Wiki sites.

[![Build and deploy](https://github.com/doofin/hugo-docs-theme/actions/workflows/hugoCD.yaml/badge.svg)](https://github.com/doofin/hugo-docs-theme/actions/workflows/hugoCD.yaml)

Features:

1. Documentation
2. Mermaid Support for diagrams and flowcharts
3. Flowcharts, Piecharts, doughnut & bar charts support
4. Gallery Support
5. Native lazy loading of images
6. Live search
7. Searchable & Sortable tables
8. Syntax highlighting
9. Tina CMS support. Ships with configuration


## Demo site
Currently deployed at github pages: https://doofin.github.io/hugo-docs-theme/
see `.github/workflows/hugoCD.yml` for deployment configuration


Try it locally:
```bash
git clone --recurse-submodules --depth 1 https://github.com/onweru/compose.git
cd compose/exampleSite/
hugo server --themesDir ../..
```

Note: You must edit `hugo.toml` to set the `theme` parameter to the directory name of the theme directory when you change themes!

The original [exampleSite](https://github.com/onweru/compose/tree/master/exampleSite) is also theme's [user guide](https://composedocs.netlify.app/docs/compose/install-theme/) .

## Deployment
Deploy to github pages, see hugo docs:
https://gohugo.io/host-and-deploy/host-on-github-pages/

Basic steps:
- configure your repo settings in github
- add a github action file under `.github/workflows/gh-pages.yml`
- change `hugo.toml` for cache


## Project architecture
Currently, the theme folder is passed as argument to hugo command rather than using hugo modules, for github pages. The `go.mod` in this repo is problematic, please refer to the upstream repo for module usage.

The theme uses the following technologies:
- sass for styling, under the `layouts/partials/head/index.html`, which invokes hugo's sass processor
- go lang for module mechanism(`go.mod` and `go.sum` files), which is used by hugo to manage themes as modules, pay attention since the module mechanism is complicated as it requires versioning

In addition, refer to **docs**: https://doofin.github.io/hugo-docs-theme/docs/compose/config/ to understand the configuration options


To learn more about directory structure, see [Hugo directory structure](https://gohugo.io/getting-started/directory-structure/)

## License

This theme is available under the [MIT license](https://github.com/onweru/compose/blob/master/LICENSE).
