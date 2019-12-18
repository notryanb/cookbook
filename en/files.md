---
layout: content
title: Files
prev: Native Programs
next: Git
link_prev: /en/native_shell_programs.html
link_next: /en/git.html
---

### Editing a file and then saving the changes

Here we are making edits to `Cargo.toml`.
We increase the patch version of the crate using `inc` and then save it back to the file.
Use `help inc` to get more information.


Read the file's initial contents

`open Cargo.toml | get package.version`

Output

`0.5.1`

Make the edit to the version number and save it.

Nu keeps track of the file you have opened.
You may omit the filename argument from `save` if you want to save the changes to the opened file.

`open Cargo.toml | inc package.version --patch | save`

Output
*none*

View the changes we made to the file.

`open Cargo.toml | get package.version`

Output

`0.5.2`


---

### Parsing a file in a non-standard format

Suppose you have a file with the following format.

```
band:album:year
Fugazi:Steady Diet of Nothing:1991
Fugazi:The Argument:2001
Fugazi:7 Songs:1988
Fugazi:Repeater:1990
Fugazi:In On The Kill Taker:1993
```

You can parse it into a table.

`open bands.txt | lines | split-column ":" Band Album Year | skip 1 | sort-by Year`

Output 

```
━━━┯━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━
 # │ Band   │ Album                  │ Year
───┼────────┼────────────────────────┼──────
 0 │ Fugazi │ 7 Songs                │ 1988
 1 │ Fugazi │ Repeater               │ 1990
 2 │ Fugazi │ Steady Diet of Nothing │ 1991
 3 │ Fugazi │ In On The Kill Taker   │ 1993
 4 │ Fugazi │ The Argument           │ 2001
━━━┷━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━
```

You can alternatively do this using `read`.

`open bands.txt | read "{Band}:{Album}:{Year}" | skip 1 | sort-by Year`

`open bands.txt | parse "{Band}:{Album}:{Year}" | skip 1 | sort-by Year` *master only*

---
