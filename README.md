# `lerr()` - `err(3)` style logging API with console and syslog backends

This API supports logging by daemons, either to syslog or
to the console. It is modelled after the API provided by the
[`err(3)`](https://man.openbsd.org/err.3) family of functions.

By default logging is output to the console via the `err(3)` API.
However, if the daemon forks, the same API can be directed to syslog.

## API

`lerr()`, `lerrx()`, `lwarn()`, and `lwarnx()` are equivalent to
`err()`, `lerr()`, `warn()`, and `warnx()` respectively.

`linfo()` and `ldebug()` can be used to log information at the
`LOG_INFO` and `LOG_DEBUG` log levels in the `syslog()` backend.
`warnx()` is used as the backend for these functions in console
logger.

`logger_syslog()` is used to switch the logger from console output
to syslog output. Internally it passes the `progname` argument as
the `ident` argument to [`openlog(3)`](https://man.openbsd.org/openlog.3).

## Examples

```c
if (!debug) {
	logger_syslog(getprogname());
}
linfo("program has started");
```
