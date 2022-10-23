![tea](https://tea.xyz/banner.png)

tea is a decentralized package manager—this requires a decentralized package
registry. Our pantries are our tentative first step towards that goal.

# What is a Pantry?

Pantries provide consistent metadata about open source packages. This
metadata shouldn’t require manual collection, but at this current state in
open source it does.

It is collected and duplicated thousands of times. A huge waste of effort.

tea aims to eradicate this wasted effort, though unfortunately, the journey
there will require—to some extent—doing that duplication one more time.

## Doing it a Little Better This Time

Our format is YAML, which is at least non-proprietary and could be used by
other tools without an independent parser. And we’re pulling in data from
other sources as much as possible, eg. versions are taken from the
“source” whenever possible.

# Today

We’re launching with two pantries:

* [pantry.core]
* [pantry.extra]

[pantry.core] is essential libraries and utilities and we intend for its
contents to always be up-to-date, well-tested and available for all our
supported platforms.

[pantry.extra] is everything else.

Submissions should go to [pantry.extra]. Once they are stable and if otherwise
deemed appropriate we will move them to [pantry.core].

# The Future

This repository ([pantry.zero]) is a stub that will only ever contain this
README. The packages contained in forks of this repo will be searchable when
using [tea/cli] itself. Thus decentralizing the upkeep of the open source
package graph.

Forks of specific pantries will also be able to inherit functionality from
those pantries.

This is not built yet, but it’s a near term goal.

# The Future, Future

We love GitHub, but it’s centralized. *Open source is too important to have a
single gatekeeper*.

[pantry.core]: https://github.com/teaxyz/pantry.core
[pantry.extra]: https://github.com/teaxyz/pantry.extra
[pantry.zero]: https://github.com/teaxyz/pantry.zero
[tea/cli]: https://github.com/teaxyz/cli
