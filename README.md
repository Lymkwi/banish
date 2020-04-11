BANISH Daemon
=============

Banish is a simple python script written to spawn a daemon and send it file paths. Those file paths are then run through the "srm" command in the background.
Currently only supports Linux and UNIX derivatives.

# Usage

Banish can be run from the CLI, using any version of Python3 above 3.7.

## Help

The help for banish is available at
```bash
banish -h
```

## Running and banishing

Spawning the server is done as follows :
```bash
banish -s
```

This opens a unix file socket which location is currently hardcoded to `/tmp/banish`

Once a daemon is launched, you can simply send as many paths as you wish.
```bash
banish Path1 Path/2 ../Even/Relative/paths
```
Note that you can also wildcards as long as they are expended by your shell. Banish will convert any relative path to absolute paths in an effort to provide functional paths to `srm` at any cost.

## Polling data

Once the daemon runs in the background, it may be useful to poll data from it. You can poll two things as of the current version of banish :

 - The trace of internal logs produced by banish (`LOG` query)
 - The size of the queue of paths to be securely deleted (`SIZE` query)

A query, or series of queries, can be summoned as follows :
```bash
banish -p QUERY1 QUERY2 QUERY3 ...
```

__Note__ : Duplicate queries are not run and queries are run in the same order they first appear in.

## Killing the daemon

The following command sends a termination sequence to the server if it is up :
```bash
banish --kill
```

This erases the file socket and frees the process. Files for which the srm process was started will be erased, but the queue after them will be purged and paths in it will not be removed.
