---
draft: false
layout: "library"
slider_enable: true
description: ""
disclaimer: "The contents of this web site and the associated <a href=\"https://github.com/pmem\">GitHub repositories</a> are BSD-licensed open source."
aliases: ["rpma_conn_cfg_new.3.html"]
title: "librpma | PMDK"
header: "librpma API version 0.14.0"
---
{{< manpages >}}

[comment]: <> (SPDX-License-Identifier: BSD-3-Clause)
[comment]: <> (Copyright 2020-2022, Intel Corporation)

NAME
====

**rpma\_conn\_cfg\_new** - create a new connection configuration object

SYNOPSIS
========

          #include <librpma.h>

          struct rpma_conn_cfg;
          int rpma_conn_cfg_new(struct rpma_conn_cfg **cfg_ptr);

DESCRIPTION
===========

**rpma\_conn\_cfg\_new**() creates a new connection configuration object
and fills it with the default values:

            .timeout_ms = 1000
            .cq_size = 10
            .rcq_size = 0
            .sq_size = 10
            .rq_size = 10
            .shared_comp_channel = false

RETURN VALUE
============

The **rpma\_conn\_cfg\_new**() function returns 0 on success or a
negative error code on failure. **rpma\_conn\_cfg\_new**() does not set
\*cfg\_ptr value on failure.

ERRORS
======

**rpma\_conn\_cfg\_new**() can fail with the following error:

-   RPMA\_E\_INVAL - cfg\_ptr is NULL

-   RPMA\_E\_NOMEM - out of memory

SEE ALSO
========

**rpma\_conn\_cfg\_delete**(3),
**rpma\_conn\_cfg\_get\_compl\_channel**(3),
**rpma\_conn\_cfg\_get\_cq\_size**(3),
**rpma\_conn\_cfg\_get\_rq\_size**(3),
**rpma\_conn\_cfg\_get\_sq\_size**(3),
**rpma\_conn\_cfg\_get\_timeout**(3),
**rpma\_conn\_cfg\_set\_compl\_channel**(3),
**rpma\_conn\_cfg\_set\_cq\_size**(3),
**rpma\_conn\_cfg\_set\_rq\_size**(3),
**rpma\_conn\_cfg\_set\_sq\_size**(3),
**rpma\_conn\_cfg\_set\_timeout**(3), **rpma\_conn\_req\_new**(3),
**rpma\_ep\_next\_conn\_req**(3), **librpma**(7) and
https://pmem.io/rpma/
