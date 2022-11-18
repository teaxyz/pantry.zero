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

&nbsp;


# Contributing

Clone the following alongside each other†:

* https://github.com/teaxyz/cli
* https://github.com/teaxyz/pantry.core
* This repo (unless this is pantry.zero obv. (this guide is *for forks*))

> † so an `ls` shows this:
> ```sh
> $ ls
> cli
> pantry.core
> pantry.foo
> ```

Keep your tea/cli checkout updated since currently there is unversioned
revlock between the two. Also you should update your installed tea/cli
frequently!)‡

> ‡ `sh <(curl tea.xyz)` updates the installed tea/cli

> Note that packages are split across multiple pantries, so to see the
> `package.yml` files for all your dependencies you may want to open another
> editor at `~/.tea/tea.xyz/var/pantry`

Create new `package.yml` files namespaced as per our current patterns under
the [`./projects/`] folder. The `package.yml` format is not documented
(sorry! we will gradually fix this!), but it is not complex, pick an existing
entry for tips.

You should verify that your package builds before submitting it.

Builds typically require the Xcode Command Line Tools
(`sudo xcode-select --install`) on macOS and `libc-dev` on Linux.

```sh
$ export GITHUB_TOKEN=…
# ^^ we need a (zero permissions) [PAT] to fetch version info from GitHub

$ export TEA_PANTRY_PATH="$PWD/pantry.foo"
# ^^ this ensures tea know about the pantry you are editing

$ pantry.core/scripts/build.ts pkg.com
# ^^ our build infra is all in pantry.core currently
```

Packages require a `test` YAML node. This script should thoroughly verify all
the functionality of the package is working. You can run the test with:

```sh
pantry.core/scripts/test.ts pkg.com
```

*You don’t have access to the sources here*—so eg. `make test` won’t work.
This is deliberate. We aren't testing the source, we’re testing the
*implementation*. You want to write a test that *uses the tool*.

tea requires all packages be relocatable and cross platform. Our CI will
verify this for you. You can check locally by moving the installation from
`~/.tea` to another tea installation (eg. `~/scratch/tea`§ and running the
test again.

Now make a pull request! We’ll test on all platforms we support in the PR. If
it passes both CI and review: we’ll merge!

> § `TEA_PREFIX=~/scratch/tea sh <(curl tea.xyz)`

## Packaging Guide

Our [wiki] is our packaging knowledge base.
For other assistance, start a [discussion].

## Build Woes?

PR on [pantry.extra] and we’ll help you out.

## After Your Contribution

We build “bottles” (tar’d binaries) and upload them to both our centralized
bottle storage and decentralized [IPFS].

tea automatically builds new releases of packages *as soon as they are
released* (usually starting the builds within seconds). There is no need to
submit PRs for updates.




[wiki]: https://github.com/teaxyz/pantry.zero/wiki
[pantry.core]: https://github.com/teaxyz/pantry.core
[pantry.extra]: https://github.com/teaxyz/pantry.extra
[pantry.zero]: https://github.com/teaxyz/pantry.zero
[tea/cli]: https://github.com/teaxyz/cli
[discussion]: https://github.com/orgs/teaxyz/discussions
[PAT]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
[IPFS]: https://ipfs.tech
[`./projects/`]: https://github.com/teaxyz/panty.core/projects
