# Problem

After installing postgres on Linux and trying to log in, I get the error
`FATAL:  Ident authentication failed for user "postgres"`

# Solution

This is due to incorrect configuration of the `pg_hba.conf` file. Follow the steps outlined in [this document](https://help.ubuntu.com/stable/serverguide/postgresql.html) 