# `resourcer` package with `RPostgres` support

This repository is a fork of the [`resourcer`](https://github.com/obiba/resourcer) package, designed to restore [`RPostgres`](https://github.com/r-dbi/RPostgres) support for PostgreSQL connections in its newer versions. Since version 1.5.0, the package transitioned to use [`RPostgreSQL`](https://github.com/tomoakin/RPostgreSQL) instead of `RPostgres` in response to [issue #10](https://github.com/obiba/resourcer/issues/10). However, `RPostgreSQL` has known compatibility issues with certain environments, as described in [this StackOverflow post](https://stackoverflow.com/a/64614787).

## Why use `RPostgres`?

`RPostgres` is recommended over `RPostgreSQL` because of its compatibility with newer versions of PostgreSQL (e.g., version 13 and above). `RPostgres` uses the `libpq` client library and the `Rcpp` package for better performance and reliability. In contrast, `RPostgreSQL` relies on an older version of `libpq`, which can cause connection and authentication issues.

Although `RPostgreSQL` is the default driver for PostgreSQL in `resourcer` and most DataSHIELD environments are suited for it, the `RPostgres` library may provide a more reliable solution for independent development and testing (e.g., when running a [`DSLite`](https://github.com/datashield/DSLite) server on a local machine). This is a temporary solution primarily intended to assist DataSHIELD package developers **who do not need schema selection features for PostgreSQL databases**.

## Installation

To install and use this version of the package, run the following command (you may need to use `force = TRUE` to overwrite the previously installed version):
```r
remotes::install_github("davidsarratgonzalez/RPostgres.resourcer", force = TRUE)
library(resourcer)
```

## Known issues

This version may still face limitations similar to those raised in the original repository, specifically with schema selection when using PostgreSQL (see [issue #10](https://github.com/obiba/resourcer/issues/10)).

For more details on the `resourcer` package, please refer to the [original package repository](https://github.com/obiba/resourcer).