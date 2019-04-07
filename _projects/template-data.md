---
layout : project
title: TemplateData
tagline: integration of template data with Lua
info :
  github :
    entries :
      - '[ldoc](TemplateData/mw.templatedata.html)'
      - '[repo](https://github.com/jeblad/TemplateData)'
description : Mediawiki extension to export TemplateData and make it available to Lua modules.
---

Fork of [Extension:TemplateData](https://www.mediawiki.org/wiki/Extension:TemplateData) for Mediawiki. This version has additional code for accessing TemplateData as Lua tables. By providing TemplateData as Lua tables they can be used by template-aware modules, and even to automate building of complete templates. An important part of this is to lower the overall work involved in setting up a new template.

If you consider using this extension, please verify that the remaining code is up to date.