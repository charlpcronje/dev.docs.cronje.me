---
title: XML::Tiny | DEVserv.ME
label: XML::Tiny
order: 39
authors:
  - name: Charl Cronje
    email: charl@devserv.me
    link: https://charl-cv.devserv.me
    avatar: https://assets.devserv.me/avatars/darker.jpg
---
## DESCRIPTION

`XML::Tiny` is a simple lightweight parser for a subset of XML

## SYNOPSIS

```perl
use XML::Tiny qw(parsefile);
open($xmlfile, 'something.xml);
my $document = parsefile($xmlfile);
```

This will leave $document looking something like this:

```perl
[
    {
        type   => 'e',
        attrib => { ... },
        name   => 'rootelementname',
        content => [
            ...
            more elements and text content
            ...
       ]
    }
]
```

See the rest at: [https://metacpan.org/pod/XML::Tiny]](https://metacpan.org/pod/XML::Tiny)
