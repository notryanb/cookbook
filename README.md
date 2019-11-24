# Nu Cookbook

This Nu Cookbook is a collection of examples to help you get the most out of using Nushell.
Unless otherwise noted,
all _recipies_ are available in the `0.5.0` version of Nu with `--all-features` enabled.
Recipies marked with  `master-only` are available when nushell is built from source using the `master` branch.

While this cookbook is a series of examples to help get you started,
you may want to review the official [nushell book](https://book.nushell.sh/) for a more comprehensive walkthrough.


## Sections
- [Setup](#setup)
- [Help](#help)
- [System](#system)
- [Files](#files)
- [Git](#git)
- [HTTP](#http)
- [Misc](#misc)


## Setup
To get the most out of nu,
it is important to setup your path and env for easy access.
There are other ways to view these values and variables,
however setting up your nu configuration will make it much easier as these are supported cross-platform.

--- 

Configure your path.

`config --set [path $nu:path]`

Output

```
━━━━━━━━━━━━━━━━━━
 path
──────────────────
 [table: 91 rows]
━━━━━━━━━━━━━━━━━━
```

---

Configure your environment variables

`config --set [env $nu:env]`

Output

```
━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━
 path             │ env
──────────────────┼────────────────
 [table: 91 rows] │ [table: 1 row]
━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━
```

---

How to list your paths

`echo $nu:path` 

or 

`config | get path`

Output

```
━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 #  │ <value>
────┼──────────────────────────────────────────────────────────────────────
  0 │ C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\
  1 │ C:\Program Files\Microsoft SQL Server\140\Tools\Binn\
  2 │ C:\Program Files\Microsoft SQL Server\140\DTS\Binn\
  3 │ C:\Program Files (x86)\Microsoft SQL Server\150\DTS\Binn\
  4 │ C:\Program Files\erl10.3\bin
  5 │ C:\Program Files (x86)\Elixir\bin
  4 │ C:\Program Files\MongoDB\Server\4.0\bin
  5 │ C:\Users\nu_shell\.cargo\bin
  6 │ C:\Program Files\PostgreSQL\9.6\bin
  7 │ C:\Program Files\PostgreSQL\9.6\lib
  8 │ C:\WINDOWS\system32\WindowsPowerShell\v1.0\
  9 │ C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common
 10 │ C:\Program Files\Common Files\Microsoft Shared\Windows Live
 11 │ C:\Program Files (x86)\Common Files\Microsoft Shared\Windows Live
 12 │ C:\Windows\system32
 13 │ C:\Windows
 14 │ C:\Windows\System32\Wbem
 15 │ C:\Windows\System32\WindowsPowerShell\v1.0\
━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

How to list your environment variables

`echo $nu:env | pivot` 

or 

`config | get env | pivot`

Output

```
━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 #  │ Column0                         │ Column1
────┼─────────────────────────────────┼──────────────────────────────────────────────────────────
  0 │ =::                             │ ::\
  1 │ ALLUSERSPROFILE                 │ C:\ProgramData
  2 │ APPDATA                         │ C:\Users\nu_shell\AppData\Roaming
  3 │ CLASSPATH                       │ .;C:\Program Files (x86)\Java\jre6\lib\ext\QTJava.zip
  4 │ COLUMNS                         │ 80
  5 │ COMPUTERNAME                    │ nu_shell
  6 │ ChocolateyInstall               │ C:\ProgramData\chocolatey
  7 │ ChocolateyLastPathUpdate        │ Sun Oct  8 16:37:30 2017
━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

How to get a single environment variable's value

`config | get env.APPDATA` 

or 

`config | get env | pick APPDATA`

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 APPDATA
───────────────────────────────────
 C:\Users\nu_shell\AppData\Roaming
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```


## Help

A good way to become familiar with all that nu has to offer is by utilizing the `help` command.

How to see all supported commands:

`help commands`

Output

```
━━━━┯━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 #  │ name        │ description
────┼─────────────┼──────────────────────────────────────────────────────────────────────────────
  0 │ append      │ Append the given row to the table
  1 │ autoview    │ View the contents of the pipeline as a table or list.
  2 │ average     │ Compute the average of a column of numerical values.
  3 │ binaryview  │ Autoview of binary data.
  4 │ cd          │ Change to a new path.
  5 │ clip        │ Copy the contents of the pipeline to the copy/paste buffer
  6 │ config      │ Configuration management.
  7 │ count       │ Show the total number of rows.
  8 │ cp          │ Copy files.
  9 │ date        │ Get the current datetime.
 10 │ debug       │ Debug input fed.
━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

To find more specific information on a command, use `help <COMMAND>`.

`help fetch`

Output

```
Load from a URL into a cell, convert to table if possible (avoid by appending '--raw')

Usage:
  > fetch <path> {flags}

parameters:
  <path> the URL to fetch the contents from

flags:
  --raw: fetch contents as text rather than a table
  ```


## System

Nu offers many commands and plugins that help navigate a command-line interface, interface with the filesystem, and monitor your system.

View all files in the current directory

`ls | where type == File`

Output 

```
━━━━┯━━━━━━━━━━━━━━━━━━━━┯━━━━━━┯━━━━━━━━━━┯━━━━━━━━━━┯━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━
 #  │ name               │ type │ readonly │ size     │ created      │ accessed     │ modified
────┼────────────────────┼──────┼──────────┼──────────┼──────────────┼──────────────┼──────────────
  0 │ .editorconfig      │ File │          │   236 B  │ 2 months ago │ 2 months ago │ 2 months ago
  1 │ .gitignore         │ File │          │   189 B  │ 2 months ago │ 2 months ago │ 2 months ago
  2 │ .gitpod.Dockerfile │ File │          │   164 B  │ a month ago  │ a month ago  │ a month ago
  3 │ .gitpod.yml        │ File │          │   803 B  │ a month ago  │ a month ago  │ a month ago
  4 │ build.rs           │ File │          │   1.2 KB │ 3 weeks ago  │ 3 weeks ago  │ 3 weeks ago
  5 │ Cargo.lock         │ File │          │ 153.7 KB │ a week ago   │ a week ago   │ a week ago
  6 │ Cargo.toml         │ File │          │   4.7 KB │ a week ago   │ a week ago   │ a week ago
  7 │ CODE_OF_CONDUCT.md │ File │          │   3.4 KB │ 2 months ago │ 2 months ago │ 2 months ago
  8 │ features.toml      │ File │          │   443 B  │ 3 weeks ago  │ 3 weeks ago  │ 3 weeks ago
  9 │ LICENSE            │ File │          │   1.1 KB │ 2 months ago │ 2 months ago │ 2 months ago
 10 │ Makefile.toml      │ File │          │   647 B  │ 2 months ago │ 2 months ago │ 2 months ago
 11 │ README.md          │ File │          │  18.3 KB │ a week ago   │ a week ago   │ a week ago
 12 │ rust-toolchain     │ File │          │    17 B  │ a month ago  │ a month ago  │ a month ago
 13 │ rustfmt.toml       │ File │          │    16 B  │ 2 months ago │ 2 months ago │ 2 months ago
━━━━┷━━━━━━━━━━━━━━━━━━━━┷━━━━━━┷━━━━━━━━━━┷━━━━━━━━━━┷━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━
```

---

View all directories in the current directory

`ls | where type == Directory`

Output

```
━━━━┯━━━━━━━━━━━┯━━━━━━━━━━━┯━━━━━━━━━━┯━━━━━━━━┯━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━
 #  │ name      │ type      │ readonly │ size   │ created      │ accessed     │ modified
────┼───────────┼───────────┼──────────┼────────┼──────────────┼──────────────┼──────────────
  0 │ .azure    │ Directory │          │   —    │ 2 months ago │ 3 weeks ago  │ 3 weeks ago
  1 │ .cargo    │ Directory │          │   —    │ 2 months ago │ 2 months ago │ 2 months ago
  2 │ .circleci │ Directory │          │   —    │ 2 months ago │ 2 months ago │ 2 months ago
  3 │ .git      │ Directory │          │ 4.1 KB │ 2 months ago │ a week ago   │ a week ago
  4 │ .github   │ Directory │          │   —    │ 2 months ago │ 2 months ago │ 2 months ago
  5 │ assets    │ Directory │          │   —    │ 2 months ago │ 2 months ago │ 2 months ago
  6 │ debian    │ Directory │          │ 4.1 KB │ 2 months ago │ a month ago  │ a month ago
  7 │ docker    │ Directory │          │ 4.1 KB │ 2 months ago │ 3 weeks ago  │ 3 weeks ago
  8 │ docs      │ Directory │          │   —    │ 2 months ago │ 3 weeks ago  │ 3 weeks ago
  9 │ images    │ Directory │          │   —    │ 2 months ago │ 2 months ago │ 2 months ago
 10 │ src       │ Directory │          │ 4.1 KB │ 2 months ago │ a week ago   │ a week ago
 11 │ target    │ Directory │          │   —    │ a week ago   │ a week ago   │ a week ago
 12 │ tests     │ Directory │          │ 4.1 KB │ 2 months ago │ a week ago   │ a week ago
━━━━┷━━━━━━━━━━━┷━━━━━━━━━━━┷━━━━━━━━━━┷━━━━━━━━┷━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━
```

---

Find processes sorted by greatest cpu utilization.

`ps | where cpu > 0 | sort-by cpu | reverse`

Output

```
━━━┯━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━
 # │ pid   │ name                  │ status  │ cpu
───┼───────┼───────────────────────┼─────────┼───────────────────
 0 │  8564 │ nu_plugin_ps.exe      │ Running │ 70.86496000000001
 1 │ 13324 │ EpicGamesLauncher.exe │ Running │ 6.141082000000000
 2 │ 21084 │ firefox.exe           │ Running │ 6.006489999999999
 3 │ 19792 │ Code.exe              │ Running │ 5.207409999999999
━━━┷━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━
```

---

Add the output of a pipeline to your clipboard.
Note, this currently needs to be string output.

`sys | get mem | to-json | clip`

Output pasted from `clip` :)

```
{"total":17125339136,"free":8653758464,"swap total":34305208320,"swap free":19703889920}
```


## Parsing

Nu offers the ability to do some basic parsing.


How to parse an arbitrary pattern from a string of text into a multi-column table.
Note that for version `0.5.0` the parsing command is called `read`, while the next version of nushell it will be renamed to `parse`.

`cargo search shells --limit 10 | lines | read "{crate_name} = {version} #{description}"`

`cargo search shells --limit 10 | lines | parse "{crate_name} = {version} #{description}"` *master-only*

Output

```
━━━┯━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 # │ crate_name         │ version                     │ description
───┼────────────────────┼─────────────────────────────┼──────────────────────────────────────────────────────────────────────────────────
 0 │ shells             │ "0.2.0"                     │  Sugar-coating for invoking shell commands directly from Rust.
 1 │ ion-shell          │ "0.0.0"                     │  The Ion Shell
 2 │ shell-words        │ "0.1.0"                     │  Process command line according to parsing rules of UNIX shell
 3 │ nu                 │ "0.5.0"                     │  A shell for the GitHub era
 4 │ dotenv-shell       │ "1.0.1"                     │  Launch a new shell (or another program) with your loaded dotenv
 5 │ shell_completion   │ "0.0.1"                     │  Write shell completion scripts in pure Rust
 6 │ shell-hist         │ "0.2.0"                     │  A CLI tool for inspecting shell history
 7 │ tokei              │ "10.0.1"                    │  A utility that allows you to count code, quickly.
 8 │ rash-shell         │ "0.1.0"                     │  A bourne-compatible shell inspired by dash
 9 │ rust_keylock_shell │ "0.10.0"                    │  Shell access to the rust-keylock. rust-keylock is a password manager with goals
   │                    │                             │ to be Secure, …
━━━┷━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Native Shell Programs
Nu allows you to access native shell programs by escaping the program name with `^`.

`sc` is a Windows CMD program that is used for communicating with the Service Control Manager

`^sc queryex eventlog | lines | trim | parse "{key}: {value}"`

Output

```
━━━┯━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━
 # │ key                 │ value
───┼─────────────────────┼────────────
 0 │ SERVICE_NAME        │ eventlog
 1 │ TYPE                │ 30  WIN32
 2 │ STATE               │ 4  RUNNING
 3 │ WIN32_EXIT_CODE     │ 0  (0x0)
 4 │ SERVICE_EXIT_CODE   │ 0  (0x0)
 5 │ CHECKPOINT          │ 0x0
 6 │ WAIT_HINT           │ 0x0
 7 │ PID                 │ 1628
━━━┷━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━
```


## Git
Nu can help with common `Git` tasks like removing all local branches which have been merged into master.

Delete git merged branches.
Warning: This command will hard delete the merged branches from your machine.
You may want to check the branches selected for deletion by omitting the last git command.

`git branch --merged | lines | where $it != "* master" | git branch -D $it`

Output

```
Deleted branch post-argument-positions (was 9d34ec9).
```

Parse formatted commit messages

`git log "--pretty=format:%h<nu>%aN<nu>%s<nu>%aD" | lines | split-column "<nu>" sha1 committer desc merged_at | first 10`


Output

```
━━━┯━━━━━━━━━┯━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 # │ hash    │ author          │ time        │ message
───┼─────────┼─────────────────┼─────────────┼──────────────────────────────────────────────────────────────────
 0 │ 9d34ec9 │ Jonathan Turner │ 13 days ago │ Merge pull request #891 from nushell/jonathandturner-patch-1
 1 │ fd92271 │ Jonathan Turner │ 13 days ago │ Move rustyline dep back to crates
 2 │ 2d44b7d │ Jonathan Turner │ 2 weeks ago │ Update README.md
 3 │ faccb06 │ Jonathan Turner │ 2 weeks ago │ Merge pull request #890 from jonathandturner/append_prepend
 4 │ a9cd6b4 │ Jonathan Turner │ 2 weeks ago │ Format files
 5 │ 81691e0 │ Jonathan Turner │ 2 weeks ago │ Add prepend and append commands
 6 │ 26f40dc │ Jonathan Turner │ 2 weeks ago │ Merge pull request #889 from jonathandturner/read_plugin
 7 │ 3820fef │ Jonathan Turner │ 2 weeks ago │ Add a simple read/parse plugin to better handle text data
 8 │ b6824d8 │ Jonathan Turner │ 2 weeks ago │ Merge pull request #886 from notryanb/fetch-from-variable
 9 │ e09160e │ Ryan Blecher    │ 2 weeks ago │ add ability to create PathBuf from string to avoid type mismatch
━━━┷━━━━━━━━━┷━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

View git comitter activity as a `histogram` *master-only*

`git log "--pretty=format:%h<nu>%aN<nu>%s<nu>%aD" | lines | split-column "<nu>" sha1 committer desc  merged_at | histogram committer merger | sort-by merger | reverse`

```
━━━━┯━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 #  │ committer           │ merger
────┼─────────────────────┼──────────────────────────────────────────────────────────────────────────────────────────────────────
  0 │ Jonathan Turner     │ ****************************************************************************************************
  1 │ Andrés N. Robalino  │ ***********************
  2 │ Yehuda Katz         │ **************
  3 │ est31               │ *****
  4 │ Thomas Hartmann     │ ****
  5 │ Sean Hellum         │ **
  6 │ Patrick Meredith    │ **
  7 │ Fahmi Akbar Wildana │ **
  8 │ Vanessa Sochat      │ *
  9 │ Shaurya Shubham     │ *
 10 │ Pirmin Kalberer     │ *
 11 │ Odin Dutton         │ *
 12 │ Jonathan Rothberg   │ *
 ━━━┷━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ```


## Files

Editing a file and then saving the changes.

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

Parsing a file in a non-standard format

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

## HTTP

Fetching JSON from a url

`fetch https://jsonplaceholder.typicode.com/posts | first 5`

Output 

```
━━━┯━━━━━━━━┯━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 # │ userId │ id │ title                                                   │ body
───┼────────┼────┼─────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────
 0 │      1 │  1 │ sunt aut facere repellat provident occaecati excepturi  │ quia et suscipit
   │        │    │ optio reprehenderit                                     │ suscipit recusandae consequuntur expedita et cum
   │        │    │                                                         │ reprehenderit molestiae ut ut quas totam
   │        │    │                                                         │ nostrum rerum est autem sunt rem eveniet architecto
 1 │      1 │  2 │ qui est esse                                            │ est rerum tempore vitae
   │        │    │                                                         │ sequi sint nihil reprehenderit dolor beatae ea dolores
   │        │    │                                                         │ neque
   │        │    │                                                         │ fugiat blanditiis voluptate porro vel nihil molestiae ut
   │        │    │                                                         │ reiciendis
   │        │    │                                                         │ qui aperiam non debitis possimus qui neque nisi nulla
 2 │      1 │  3 │ ea molestias quasi exercitationem repellat qui ipsa sit │ et iusto sed quo iure
   │        │    │ aut                                                     │ voluptatem occaecati omnis eligendi aut ad
   │        │    │                                                         │ voluptatem doloribus vel accusantium quis pariatur
   │        │    │                                                         │ molestiae porro eius odio et labore et velit aut
 3 │      1 │  4 │ eum et est occaecati                                    │ ullam et saepe reiciendis voluptatem adipisci
   │        │    │                                                         │ sit amet autem assumenda provident rerum culpa
   │        │    │                                                         │ quis hic commodi nesciunt rem tenetur doloremque ipsam
   │        │    │                                                         │ iure
   │        │    │                                                         │ quis sunt voluptatem rerum illo velit
 4 │      1 │  5 │ nesciunt quas odio                                      │ repudiandae veniam quaerat sunt sed
   │        │    │                                                         │ alias aut fugiat sit autem sed est
   │        │    │                                                         │ voluptatem omnis possimus esse voluptatibus quis
   │        │    │                                                         │ est aut tenetur dolor neque
━━━┷━━━━━━━━┷━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

Suppose you are querying several endpoints, 
perhaps with different query parameters and you want to view all the responses as a single dataset.
You can make use of `$it` to run nu commands on every row of data.

An example JSON file, `urls.json`, with the following contents:

```
{
  "urls": [
    "https://jsonplaceholder.typicode.com/posts/1",
    "https://jsonplaceholder.typicode.com/posts/2",
    "https://jsonplaceholder.typicode.com/posts/3"
  ]
}
```

`open urls.json | get urls | fetch $it`

Output

```
━━━┯━━━━━━━━┯━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 # │ userId │ id │ title                                                   │ body
───┼────────┼────┼─────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────
 0 │      1 │  1 │ sunt aut facere repellat provident occaecati excepturi  │ quia et suscipit
   │        │    │ optio reprehenderit                                     │ suscipit recusandae consequuntur expedita et cum
   │        │    │                                                         │ reprehenderit molestiae ut ut quas totam
   │        │    │                                                         │ nostrum rerum est autem sunt rem eveniet architecto
 1 │      1 │  2 │ qui est esse                                            │ est rerum tempore vitae
   │        │    │                                                         │ sequi sint nihil reprehenderit dolor beatae ea dolores
   │        │    │                                                         │ neque
   │        │    │                                                         │ fugiat blanditiis voluptate porro vel nihil molestiae ut
   │        │    │                                                         │ reiciendis
   │        │    │                                                         │ qui aperiam non debitis possimus qui neque nisi nulla
 2 │      1 │  3 │ ea molestias quasi exercitationem repellat qui ipsa sit │ et iusto sed quo iure
   │        │    │ aut                                                     │ voluptatem occaecati omnis eligendi aut ad
   │        │    │                                                         │ voluptatem doloribus vel accusantium quis pariatur
   │        │    │                                                         │ molestiae porro eius odio et labore et velit aut
━━━┷━━━━━━━━┷━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

If you specify the `--raw` flag, you'll see 3 separate json objects, one in each row.

`open urls.json | get urls | fetch $it --raw`

Output

```
━━━┯━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 # │ <value>
───┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
 0 │ {
   │   "userId": 1,
   │   "id": 1,
   │   "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
   │   "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum
   │ rerum est autem sunt rem eveniet architecto"
   │ }
 1 │ {
   │   "userId": 1,
   │   "id": 2,
   │   "title": "qui est esse",
   │   "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro
   │ vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
   │ }
 2 │ {
   │   "userId": 1,
   │   "id": 3,
   │   "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
   │   "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis
   │ pariatur\nmolestiae porro eius odio et labore et velit aut"
   │ }
━━━┷━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

To combine these responses together into a valid JSON array, you can turn the table into json.

`open urls.json | get urls | fetch $it | to-json`

Output

```
[{"userId":1,"id":1,"title":"sunt aut facere repellat provident occaecati excepturi optio reprehenderit","body":"quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"},{"userId":1,"id":2,"title":"qui est esse","body":"est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"},{"userId":1,"id":3,"title":"ea molestias quasi exercitationem repellat qui ipsa sit aut","body":"et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"}]
```

---

Making a `post` request to an endpoint with a JSON payload.
To make long requests easier,
you can organize your json payloads inside a file.

```json
{
  "my_payload": {
    "title": "foo",
    "body": "bar",
    "userId": 1
  }
}
```

`open payload.json | get my_payload | post https://jsonplaceholder.typicode.com/posts $it`

Output

```
━━━━━
 id
─────
 101
━━━━━
```

---

We can put this all together into a pipeline where we read data, manipulate it, and then send it back to the API.
Lets `fetch` a post, `increment` the id, and `post` it back to the endpoint.
In this particular example, the test endpoint gives back an arbitrary response which we can't actually mutate.

`open urls.json | get urls | first | fetch $it | inc id | to-json | post https://jsonplaceholder.typicode.com/posts $it`

```
━━━━━
 id
─────
 101
━━━━━
```


## Misc

- To finish or "accept" an autocomplete command, press the right arrow key.
