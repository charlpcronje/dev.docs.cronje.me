---
title: Variable Variables | DEVserv.ME
label: SVariable Variables
order: 52
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
---

```perl
use strict;
use warnings;
use 5.10.0;

our $x = '5';
my $field_name = 'x';

my $contents;
{ # no strict is lexially scoped
    no strict 'refs';
    $contents = ${$field_name};
}
```