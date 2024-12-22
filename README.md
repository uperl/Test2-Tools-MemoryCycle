# Test2::Tools::MemoryCycle ![static](https://github.com/uperl/Test2-Tools-MemoryCycle/workflows/static/badge.svg) ![linux](https://github.com/uperl/Test2-Tools-MemoryCycle/workflows/linux/badge.svg)

Check for memory leaks and circular memory references

# SYNOPSIS

```perl
use Test2::V0;
use Test2::Tools::MemoryCycle;

my $foo = { bar => 1 };

memory_cycle_ok $foo;  # pass

$foo->{baz} = sub {
  print $foo->{bar}, "\n";
};

memory_cycle_ok $foo;  # fail

done_testing;
```

# DESCRIPTION

Perl's garbage collection has one big problem: Circular references can't get cleaned up.
The above example is the sort of thing that sometimes trips me up, where a code reference
inside a data structure refers to another part of the data structure.  There already
exists a good testing module to find these sort of problems: [Test::Memory::Cycle](https://metacpan.org/pod/Test::Memory::Cycle),
so why write this one?  Well that module uses [Test::Builder](https://metacpan.org/pod/Test::Builder), and this one instead uses
[Test2::API](https://metacpan.org/pod/Test2::API).  If you want to write [Test2::Suite](https://metacpan.org/pod/Test2::Suite) tests without pulling in [Test::Builder](https://metacpan.org/pod/Test::Builder)
then this is the cycle testing module for you.

This module also uses the standard [Exporter](https://metacpan.org/pod/Exporter) interface, instead of letting you specify
a test plan.  That behavior was once in vogue I guess, but I do not care for it.

# FUNCTIONS

## memory\_cycle\_ok

```
memory_cycle_ok $reference, $message;
memory_cycle_ok $reference;
```

Checks that `$reference` doesn't have any circular memory references.

# CAVEATS

This module is based on and quite similar to [Test::Memory::Cycle](https://metacpan.org/pod/Test::Memory::Cycle).  That module is
more mature, and has more features.  So far I only need the one test function.  Other
features may be added in the future.

# SEE ALSO

- [Test::Memory::Cycle](https://metacpan.org/pod/Test::Memory::Cycle)
- [Devel::Cycle](https://metacpan.org/pod/Devel::Cycle)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2022-2024 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
