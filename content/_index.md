+++
title = "ecofunctor"
[data]
baseChartOn = 3
colors = ["#627c62", "#11819b", "#ef7f1a", "#4e1154"]
columnTitles = ["Section", "Status", "Author"]
title = "Projects"
+++

The Scala platforms:

{{< mermaid >}}
graph TB
  Scala-->Sc(Scala Jvm)
  Scala-->ScJS(Scala.js)
  Scala-->ScNative(Scala Native)
{{< /mermaid >}}

## About

We are a group of Scala enthusiasts focusing on functional programming and Scala. It's been 2 years since our last meetup in Beijing on November 2023. Not just Scala, the popularity of meetups has decreased both domestically and internationally in recent years. However, as the most industrialized functional programming language, Scala has found new applications in AI, chip design, and other fields beyond big data and backend development. For more details, see our previous meetups.

Areas of interest, but not limited to:
- Domain specific languages(DSLs), like Chisel
- Compiler design(MLIR, etc)
- Mathematics, Algebraic programming
- Formal verification
- Visualization, Frontend development with Scala.js


## Contributors 
See our [repo](https://github.com/fp-meetup/scala-meetup) for details.

{{< tip >}}
Feel free to open a [PR](https://github.com/fp-meetup/scala-meetup) to add more information about the meetup.
{{< /tip >}}

## About this site
This website is built with github actions and [Hugo](https://gohugo.io/) static site generator, It's automatically deployed to GitHub pages when changes are pushed to the main branch. The theme is a fork of [Compose](https://github.com/doofin/hugo-docs-theme)