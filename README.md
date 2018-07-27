LERR(3) - Library Functions Manual

# NAME

**lerr**,
**lerrx**,
**lwarn**,
**lwarnx**,
**linfo**,
**ldebug**,
**logger\_syslog** - Logging API for daemons

# SYNOPSIS

**#include &lt;log.h>**

*void*  
**lerr**(*int ecode*, *const char \*fmt*, *...*);

*void*  
**lerrx**(*int ecode*, *const char \*fmt*, *...*);

*void*  
**lwarn**(*const char \*fmt*, *...*);

*void*  
**lwarnx**(*const char \*fmt*, *...*);

*void*  
**linfo**(*const char \*fmt*, *...*);

*void*  
**ldebug**(*const char \*fmt*, *...*);

*void*  
**logger\_syslog**(*const char \*progname*);

# DESCRIPTION

This API supports logging by daemons, either to syslog or
to the console.

By default logging is output to the console via the
err(3)
and
warn(3)
family of functions.
However, if the daemon forks, the same API can be directed to syslog.

**lerr**,
**lerrx**,
**lwarn**,
and
**lwarnx**
are equivalent to
err(3),
errx(3),
warn(3),
and
warnx(3)
respectively.

**linfo**
and
**ldebug**
can be used to log information at the
`LOG_INFO`
and
log levels.
warnx(3)
is used as the backend for these functions in console logger.

**logger\_syslog**
is used to switch the logger from console output to using syslog.
Internally it passes the
*progname*
argument as the ident argument to
openlog(3).

# EXAMPLES

	if (!debug) {
		logger_syslog(getprogname());
	}
	linfo("program has started");

# SEE ALSO

err(3),
syslog(3)

OpenBSD 6.3 - August 29, 2017
