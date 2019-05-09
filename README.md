# Perl template for OpenFaaS

This repository contains a Perl language template for OpenFaaS developed by the community. If you wish to make suggestions or improvements, please propose them with an issue in this repository.

## Trying the template

```bash
faas template pull https://github.com/openfaas-incubator/perl-template
faas new --lang perl hello-perl
```

This will generate:

```sh
hello-perl.yml
hello-perl/Handler.pm
```

You can then implement your handler:

```perl
package Handler;
use strict;
use warnings;

sub handle {
    my $st = shift;
    return "Hello $st !";
}

1;
```

Finally, when ready run `faas-cli up -f hello-perl`.


