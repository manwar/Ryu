# NAME

Ryu - asynchronous stream building blocks

# SYNOPSIS

    #!/usr/bin/env perl
    use strict;
    use warnings;
    use Ryu qw($ryu);
    my ($lines) =
           $ryu->from(\*STDIN)
                   ->by_line
                   ->filter(qr/\h/)
                   ->count
                   ->get;
    print "Had $lines line(s) containing whitespace\n";

# DESCRIPTION

Provides data flow processing for asynchronous coding purposes. It's a bit like [ReactiveX](https://reactivex.io) in
concept. Where possible, it tries to provide a similar API. It is not a directly-compatible implementation, however.

## Why would I be using this?

Eventually some documentation pages might appear, but at the moment they're unlikely to exist.

- Network protocol implementations - if you're bored of stringing together `substr`, `pack`, `unpack`
and `vec`, try [Ryu::Manual::Protocol](https://metacpan.org/pod/Ryu::Manual::Protocol)
- Extract, Transform, Load workflows (ETL) - need to pull data from somewhere, mangle it into shape, push it to
a database? that'd be [Ryu::Manual::ETL](https://metacpan.org/pod/Ryu::Manual::ETL)
- Reactive event handling - [Ryu::Manual::Reactive](https://metacpan.org/pod/Ryu::Manual::Reactive)

As an expert software developer with a keen eye for useful code, you may already be bored of this documentation
and on the verge of reaching for alternatives. The ["SEE ALSO"](#see-also) section may speed you on your way.

## Components

### Sources

A source emits items. See [Ryu::Source](https://metacpan.org/pod/Ryu::Source).

Items can be any scalar value - some examples:

- a single byte
- a character
- a byte string
- a character string
- an object instance
- an arrayref or hashref

### Sinks

A sink receives items. It's the counterpart to a source. See [Ryu::Sink](https://metacpan.org/pod/Ryu::Sink).

### Streams

A stream is a thing with a source. See [Ryu::Stream](https://metacpan.org/pod/Ryu::Stream), which is likely to be something that does not yet
exist.

## What does this module do?

Nothing. It's just a top-level loader for pulling in all the other components.

## Some notes that might not relate to anything

With a single parameter, ["from"](#from) and ["to"](#to) will use the given
instance as a [Ryu::Source](https://metacpan.org/pod/Ryu::Source) or [Ryu::Sink](https://metacpan.org/pod/Ryu::Sink) respectively.

Multiple parameters are a shortcut for instantiating the given source
or sink:

    my $stream = Ryu::Stream->from(
     file => 'somefile.bin'
    );

is equivalent to

    my $stream = Ryu::Stream->from(
     Ryu::Source->new(
      file => 'somefile.bin'
     )
    );

# Why the name?

- ` $ryu ` lines up with typical 4-character indentation settings.
- there's Rx for other languages, and this is based on the same ideas
- 流 was too hard for me to type

## from

Helper method which returns a [Ryu::Source](https://metacpan.org/pod/Ryu::Source) from a list of items.

## just

Helper method which returns a single-item [Ryu::Source](https://metacpan.org/pod/Ryu::Source).

# SEE ALSO

## Other modules

Some perl modules of relevance:

- [Future](https://metacpan.org/pod/Future) - fundamental building block for one-shot tasks
- [POE::Filter](https://metacpan.org/pod/POE::Filter) - venerable and battle-tested, but slightly short on features due to the focus on protocols
- [Data::Transform](https://metacpan.org/pod/Data::Transform) - standalone version of [POE::Filter](https://metacpan.org/pod/POE::Filter)
- [List::Gen](https://metacpan.org/pod/List::Gen) - list mangling features
- [HOP::Stream](https://metacpan.org/pod/HOP::Stream) - based on the Higher Order Perl book
- [Flow](https://metacpan.org/pod/Flow) - quite similar in concept to this module, maybe a bit short on documentation, doesn't provide integration with other sources such as files or [IO::Async::Stream](https://metacpan.org/pod/IO::Async::Stream)
- [Flux](https://metacpan.org/pod/Flux) - more like the java8 streams API, sync-based
- [Message::Passing](https://metacpan.org/pod/Message::Passing) - on initial glance seemed more of a commandline tool, sadly based on [AnyEvent](https://metacpan.org/pod/AnyEvent)
- [Rx.pl](https://github.com/eilara/Rx.pl) - a Perl version of the [http://reactivex.io](http://reactivex.io) Reactive API
- [Perlude](https://metacpan.org/pod/Perlude) - combines features of the shell / UNIX streams and Haskell, pipeline
syntax is "backwards" (same as grep/map chains in Perl)
- [IO::Pipeline](https://metacpan.org/pod/IO::Pipeline)
- [DS](https://metacpan.org/pod/DS)
- [Evo](https://metacpan.org/pod/Evo)
- [Async::Stream](https://metacpan.org/pod/Async::Stream) - early release, but seems to be very similar in concept to [Ryu::Source](https://metacpan.org/pod/Ryu::Source)
- [Data::Monad](https://metacpan.org/pod/Data::Monad)

## Other references

There are various documents, specifications and discussions relating to the concepts we use. Here's a few:

- [http://www.reactivemanifesto.org/](http://www.reactivemanifesto.org/)
- Java 8 [streams API](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)
- C++ [range-v3](https://github.com/ericniebler/range-v3)

# AUTHOR

Tom Molesworth <TEAM@cpan.org>

# LICENSE

Copyright Tom Molesworth 2011-2019. Licensed under the same terms as Perl itself.
