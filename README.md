# About
Play around with `yarn version` commands, understand their implications on your and make the best use of them.

# What you will already find here

A series of `yarn version` commands executed, the intent behind them and the outcome.

# Ok lets see some commands

## The Apprentice

> Q: I am just starting with the repo (i.e. v0.0.0), got code some code out towards minor changes. But I am not sure if my changes work in integration with changes from my teammates. How do I tag my latest commit to master?

> A: A preminor version is ideal in this case. "Pre" because its a pre-release, as in "I dont know if its stable, yet", minor because you described your changes as minor. Just use premajor or prepatch depending on your (real) scenario.

### Command

`yarn version --preminor`

### Expectations

The tag created is for the "next minor release", but a pre-release instead of an actual release

### Outcome

```bash
yarn version v1.22.5
info Current version: 0.0.0
info New version: 0.1.0-0
Done in 0.12s.
```

## The Apprentice wants some soda

> Q: We did some tests on top of that and guess what my changes have some bugs. I fixed them alright, how do I tag to let people/bots know my fixes are ready?

> A: Another prelease is all you need

### Command

`yarn version --prerelease`

### Expectations

A step closer to moon, i.e. v0.1.0-1

### Outcome

```bash
yarn version v1.22.5
info Current version: 0.1.0-0
info New version: 0.1.0-1
Done in 0.10s.
```

## Enter Journeyman

> Q: Isnt it kinda dumb that I am not able to tell who the pre-release is for? My CICD bots can pull plates out of the window, but they need to be told if its for table dev, or table QA or table user. Any thoughts?

> A: Use a "preid" with a pre-release. Make your bots filter for the preid, good luck with their smartness. Heres a bunch of commands to get you going.


### Command

`yarn version --prerelease --preid dev`

### Expectations

A Pre-release for the dev phase (really?).

### Outcome

```bash
yarn version v1.22.5
info Current version: 0.1.0-1
info New version: 0.1.0-dev.0
Done in 0.12s.
```
### Command

`yarn version --prerelease --preid dev`

### Expectations

The next Pre-release for the  dev team.

### Outcome

```bash
yarn version v1.22.5
info Current version: 0.1.0-dev.0
info New version: 0.1.0-dev.1
Done in 0.12s.
```

### Command

`yarn version --prerelease --preid sit`

### Expectations

A Pre-release for the integration test phase.

### Outcome

```bash
yarn version v1.22.5
info Current version: 0.1.0-dev.1
info New version: 0.1.0-sit.0
Done in 0.14s.
```

### Command

`git tag --list`

### Expectations

Lets see where that took us so far

### Outcome

```bash
v0.1.0-0
v0.1.0-1
v0.1.0-dev.0
v0.1.0-dev.1
v0.1.0-sit.0
```

### Enough with this just get through with the rest of the commands

`yarn version --prerelease --preid sit`

```bash
yarn version v1.22.5
info Current version: 0.1.0-sit.0
info New version: 0.1.0-sit.1
Done in 0.10s.
```

`yarn version --prerelease --preid uat`

```bash
yarn version v1.22.5
info Current version: 0.1.0-sit.1
info New version: 0.1.0-uat.0
Done in 0.11s.
```

`git tag --list`

```bash
v0.1.0-0
v0.1.0-1
v0.1.0-dev.0
v0.1.0-dev.1
v0.1.0-sit.0
v0.1.0-sit.1
v0.1.0-uat.0
```

`yarn version --prerelease --preid uat`

```bash
yarn version v1.22.5
info Current version: 0.1.0-uat.0
info New version: 0.1.0-uat.1
Done in 0.12s.
```

`git tag --list`

```bash
v0.1.0-0
v0.1.0-1
v0.1.0-dev.0
v0.1.0-dev.1
v0.1.0-sit.0
v0.1.0-sit.1
v0.1.0-uat.0
v0.1.0-uat.1
```


`yarn version --minor`

```bash
yarn version v1.22.5
info Current version: 0.1.0-uat.1
info New version: 0.1.0
Done in 0.10s.
```

`git tag --list`

```bash
v0.1.0
v0.1.0-0
v0.1.0-1
v0.1.0-dev.0
v0.1.0-dev.1
v0.1.0-sit.0
v0.1.0-sit.1
v0.1.0-uat.0
v0.1.0-uat.1
```

### Bonus

Tags are not listed in any (relevant) order by git. `git log` does a better job with the chronology, most recent first

`git log`

```bash
commit bdf0771e0a8538fe73666b4e42960340a3fd3281 (HEAD -> master, tag: v0.1.0)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:55:49 2020 +0530

    v0.1.0

commit 8e93f3029996504ec66441f0f1d57e3409060a1d (tag: v0.1.0-uat.1)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:53:49 2020 +0530

    v0.1.0-uat.1

commit bb6fd3b4eb887d2d4674da8c6f7434908da2a03c (tag: v0.1.0-uat.0)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:32:08 2020 +0530

    v0.1.0-uat.0

commit 02fde47a1eee780a4c13ace50e4985a95b02c896 (tag: v0.1.0-sit.1)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:19:26 2020 +0530

    v0.1.0-sit.1

commit fb6b3fc9c53fba5efa5fb10ba9442d351b856236 (tag: v0.1.0-sit.0)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:17:23 2020 +0530

    v0.1.0-sit.0

commit 6e8297176660275aaa32819f6f75c6e50f39498d (tag: v0.1.0-dev.1)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:16:51 2020 +0530

    v0.1.0-dev.1

commit 9555da83e4442d4413e57def440b5d52bb959299 (tag: v0.1.0-dev.0)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:16:02 2020 +0530

    v0.1.0-dev.0

commit a5216676312224d5efd1d02aeb6825a3a0d5a645 (tag: v0.1.0-1)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:14:06 2020 +0530

    v0.1.0-1

commit 4cddb5b46d7894cc8d1dc9511a0664acd8f2ae1d (tag: v0.1.0-0)
Author: Soumik Mukherjee <60540758+soumik-mukherjee@users.noreply.github.com>
Date:   Sat Sep 5 18:12:52 2020 +0530

    v0.1.0-0
```

