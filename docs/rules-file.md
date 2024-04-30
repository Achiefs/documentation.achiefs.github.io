---
layout: default
title: Rules file
nav_order: 4
---

# Rules file
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# File Integrity Monitor Ruleset

If you want to customize your installation and trigger custom events in addition to the given ones. It is required to edit the `rules.yml` file located at `C:\Program Files\File Integrity Monitor\rules.yml` (Windows systems) or `/etc/fim/rules.yml` (Unix systems).

In the following sections, you could review each section and parameters to tune up your ruleset as you require.

---

# Parameters
- ## rules

    Array
    {: .label .label-yellow }

    Defines an array of rules to trigger events.

    - ### id

    Integer
    {: .label .label-purple }


    A user defined integer to manage rules order and distinction. Unique value. Writing two rules with the same ID will produce unexpected results.

    - ### path

    String
    {: .label }

    Path that links the rule to the events, this path must be exactly the same as set on audit or monitor configuration sections.

    - ### rule

    String
    {: .label }

    Defines the rule to trigger this rule event, Rust regex format.

    It is sanitized from forbidden chars like `:` or `|`.

    - ### message 

    String
    {: .label }

    Message related to this rule event, it will be inside events.json schema.

---

## Example configuration

FIM comes with a ready-to-use rules file. You can tune up as you wish. Here you can see an example configuration:

Windows systems:
```
rules:
  - id: 1
    path: C:\
    rule: '\.ps1$'
    message: "Powershell script present in root directory."
  - id: 2
    path: C:\tmp
    rule: '\d'
    message: "File with digits in temp folder."
```

Linux systems:
```
rules:
  - id: 1
    path: /etc
    rule: '\.sh$'
    message: "Shell script present in /etc folder."
  - id: 2
    path: /tmp
    rule: '\d'
    message: "File with digits in temp folder."
```

macOS systems:
```
rules:
  - id: 1
    path: /etc
    rule: '\.sh$'
    message: "Shell script present in /etc folder."
  - id: 2
    path: /tmp
    rule: '\d'
    message: "File with digits in temp folder."
```
