---
title: "libpmemlog | PMDK"
draft: false
slider_enable: true
# Page title background image
bg_image: '/images/backgrounds/faq_header.jpg'
# Header
header: "libpmemlog"
# Description
description: ""
disclaimer: "The contents of this web site and the associated <a href=\"https://github.com/pmem\">GitHub repositories</a> are BSD-licensed open source."
---
### The libpmemlog library

**libpmemlog** implements a pmem-resident log file.

This library is provided for cases requiring an append-mostly
file to record variable length entries.  Most
developers will find higher level libraries like
[libpmemobj](../libpmemobj) to be more generally useful.

Man pages that contains a list of the **Linux** interfaces provided:

* Man page for <a href="../manpages/linux/master/libpmemlog/libpmemlog.7.html">libpmemlog current master</a>


Man pages that contains a list of the **Windows** interfaces provided:

* Man page for <a href="../manpages/windows/master/libpmemlog/libpmemlog.7.html">libpmemlog current master</a>

### libpmemlog Examples

#### More Detail Coming Soon

{{< highlight c "linenos=true,hl_lines=7,linenostart=37" >}}
#include <stdio.h>
#include <fcntl.h>
#include <errno.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <libpmemlog.h>

/* size of the pmemlog pool -- 1 GB */
#define	POOL_SIZE ((off_t)(1 << 30))

/*
 * printit -- log processing callback for use with pmemlog_walk()
 */
int
printit(const void *buf, size_t len, void *arg)
{
	fwrite(buf, len, 1, stdout);
	return 0;
}

int
main(int argc, char *argv[])
{
	const char path[] = "/pmem-fs/myfile";
	PMEMlogpool *plp;
	size_t nbyte;
	char *str;

	/* create the pmemlog pool or open it if it already exists */
	plp = pmemlog_create(path, POOL_SIZE, 0666);

	if (plp == NULL)
	    plp = pmemlog_open(path);

	if (plp == NULL) {
		perror(path);
		exit(1);
	}

	/* how many bytes does the log hold? */
	nbyte = pmemlog_nbyte(plp);
	printf("log holds %zu bytes\n", nbyte);

	/* append to the log... */
	str = "This is the first string appended\n";
	if (pmemlog_append(plp, str, strlen(str)) < 0) {
		perror("pmemlog_append");
		exit(1);
	}
	str = "This is the second string appended\n";
	if (pmemlog_append(plp, str, strlen(str)) < 0) {
		perror("pmemlog_append");
		exit(1);
	}

	/* print the log contents */
	printf("log contains:\n");
	pmemlog_walk(plp, 0, printit, NULL);

	pmemlog_close(plp);
}
{{< /highlight >}}