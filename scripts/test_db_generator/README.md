This is a quick and dirty go script for generating a contrived database for testing purposes.

Edit the `config.yml` file to your liking. The numbers indicate the number of objects to generate, the `naming` section indicates the files from which to generate names.

May cause unexpected behaviour if run against an existing database file.

To run - from the `test_db_generator` directory:
`go run -tags "tools sqlite_stat4 sqlite_math_functions" .`

The `tools` tag is required because the sources are behind a `//go:build tools` constraint;
the sqlite tags match the ones the main build uses (see `BUILD_TAGS` in the Makefile) so that
the generated database behaves the same as one produced by stash itself.

The database file will be generated in the current directory.

Note that the database is left with an active write-ahead log. When inspecting the result with
the `sqlite3` CLI, do not open it with `immutable=1` - that skips the WAL and will report stale
(or zero) row counts for whatever was written last.
