---
layout : project
title: Expect
tagline: a Lua assertion framework for Mediawiki
info :
  github :
    entries :
    - '[repo](https://github.com/jeblad/Expect/)'
    - '[ldoc](/Expect/)'
description : 'Mediawiki extension providing an assertion framework for the Lua programming language.'
---

The [Expect extension](https://mediawiki.org/wiki/Extension:Expect) for Mediawiki adds an assertion framework to Lua modules run by the [Scribunto extension](https://mediawiki.org/wiki/Extension:Scribunto). An integral part is to report failures clearly and visible to facilitate interactive and collaborative fault fixing, by adding extended assertions that can detect far more faults with finer granularity. It can also be set up to give more descriptive feedback. An important end result of using this extension is to create code with fewer faults.