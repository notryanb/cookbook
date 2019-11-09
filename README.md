# Nu Cookbook

This Nu Cookbook is a collection of examples to help you get the most out of using Nushell.
All the _recipies_ are available in the `0.5.0` version of Nu with `--all-features` enabled.


## Nu Setup

To get the most out of nu,
it is important to setup your path and env for easy access.
There are ways to view these values and variable,
but setting up your nu configuration will make it much easier as these are supported cross-platform.

Configure your path.
> config --set [path $nu:path]

Configure your environment variables
> config --set [env $nu:env]

How to list your paths

> config | get path

How to list your environment variables

> config | get env | pivot


## Help

A good way to become familiar with all that nu has to offer is by utilizing the `help` command.

How to see all supported commands:

> help commands

To find more specific information on a command, use `help <COMMAND>`.

> help ps

## System

Nu offers many commands and plugins that help navigate a command-line interface, interface with the filesystem, and monitor your system.

View all files in the current directory

> ls | where type == File

View all directories in the current directory

> ls | where type == Directory

List path on macOS or Linux, if you have not set up your nu `config`

> env | get vars.PATH | split-row ":"

List path on Windows, if you have not set up your nu `config`

> env | get vars.Path | split-row ";"

Find processes sorted by greatest cpu utilization.

> ps | where cpu > 0 | sort-by cpu | reverse


## Parsing

Nu supports calling executable available on your system and operating on their output.

Split output of cargo search by crate name, version, and dependency.

> cargo search shells --limit 10 | lines | read "{crate_name} = {value} #{description}" 


## Git

Delete git merged branches.

> git branch --merged | lines | where $it != "* master" | git branch -D $it


## Manipulating Files

Incrementing the version of a Rust crate.

> open "Cargo.toml" | inc package.version | save "Cargo_new.toml"


## HTTP

Fetching JSON from a url

> fetch https://jsonplaceholder.typicode.com/posts

Suppose you are querying several endpoints, 
perhaps with different query parameters and you want to view all the responses as a single dataset.
You can make use of `$it` to run nu commands on every row of data.

An example JSON file, `urls,json`, with the following contents:

```
{
  "urls": [
    "https://jsonplaceholder.typicode.com/posts/1",
    "https://jsonplaceholder.typicode.com/posts/2",
    "https://jsonplaceholder.typicode.com/posts/3"
  ]
}
```

> open urls.json | fetch $it


If you specify the `--raw` flag, you'll see 3 separate json objects, one in each row.

> open urls.json | fetch $it --raw


To combine these responses together into a valid JSON array, you can turn the table into json.

> open urls.json | fetch | to-json


Making a `post` request to an endpoint with a JSON payload.
To make long requests easier,
you can organize your json payloads inside a file.

```json
{
  "my_payload" {
    "title": "foo",
    "body": "bar",
    "userId": 1
  }
}
```

> open urls.json | post https://jsonplaceholder.typicode.com/posts $it.my_payload


We can put this all together into a pipeline where we read data, manipulate it, and then send it back to the API.
Lets `fetch` a post, `increment` the id, and `post` it back to the endpoint.

> open urls.json | get urls | first | fetch $it | inc id | to-json | post http://jsonplaceholder.typicode.com/posts $it
