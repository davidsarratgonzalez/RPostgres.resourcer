# Resource R

[![Build Status](https://travis-ci.com/obiba/resourcer.svg?branch=master)](https://travis-ci.com/obiba/resourcer)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/resourcer)](https://cran.r-project.org/package=resourcer)

The `resourcer` package is meant for accessing resources identified by a URL in a uniform way whether it references a dataset (stored in a file, a SQL table, a MongoDB collection etc.) or a computation unit (system commands, web services etc.). Usually some credentials will be defined, and an additional data format information can be provided to help dataset coercing to a data.frame object.

Currently supported data formats are the ones that have a reader in [tidyverse](https://www.tidyverse.org/): [readr](https://readr.tidyverse.org/) (`csv`, `csv2`, `tsv`), [haven](https://haven.tidyverse.org/) (`spss`, `sav`, `por`, `dta`, `stata`, `sas`, `xpt`), [readxl](https://readxl.tidyverse.org/) (`excel`, `xls`, `xlsx`).

Usage example that reads a local SPSS file:

```r
# make a SPSS file resource
res <- resourcer::newResource(
  name = "CNSIM1",
  url = "file:///data/CNSIM1.sav",
  class = "spss"
)

# coerce the csv file in the opal server to a data.frame
df <- as.data.frame(res)
```

Another example that connects to a computation server through SSH:

```r
# make an application resource on a ssh server
res <- resourcer::newResource(
  name = "supercomp1",
  url = "ssh://server1.example.org/work/dir?exec=plink,ls",
  identity = "sshaccountid",
  secret = "sshaccountpwd",
  class = NULL
)

# get ssh client from resource object
resolver <- SshResolver$new()
client <- resolver$newClient(res) # does a ssh::ssh_connect()

# execute commands
files <- client$exec("ls") # exec 'cd /work/dir && ls'

# release connection
client$close() # does ssh::ssh_disconnect(session)
```
