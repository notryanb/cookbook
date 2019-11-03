# Some Scratch One liners to sort through.

If you want to clean out git branches that have already merged:

> git branch --merged | lines | where $it != "* master" | git branch -D $it



Search on cargo and map the lines
> cargo  search github --limit 1000 | lines | first 99 | read "{Name} = {Value} #{Description}" | sort-by Name
> cargo  search github --limit 25 | lines | read "{Name} = {Value} #{Description}" 

# Windows

How to run Windows shell scripts, with $it and piping the results into a table 
> which az | cmd /c $it keyvault show -n my-keyvault | from-json

pretty print path
> env | get vars | get Path | split-row ";"

## macOS

pretty print path
> env | get vars | get PATH | split-row ":"


## Ideas

Download a graph api query multiple ways from settings file and output to json