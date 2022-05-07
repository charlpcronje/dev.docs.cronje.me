---
title: Argument Parsing Sub-Routines | CRONje.ME
label: Argument Parsing SR
order: 60
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://charl-cv.CRONje.ME
    avatar: https://assets.CRONje.ME/avatars/darker.jpg
---

```perl
my %args  = @_ && ref $_[0] eq 'HASH' ? %{ $_[0] } : @_;
    bless { %args }, $class;
```
