---
layout: default
title: Project Status
parent: Supplier Prospectus
nav_order: 3
last_modified_date:  2020-11-08 15:26:12 UTC
share: Prototyping a Supplier Prospectus
---

# Project Status
{: .no_toc }


We've made the application operational in a live environment it is 
[available for testing](../try-it/).
{: .fs-5 .fw-300 }

---


### Completed modules

Data from the [System for Award Management (SAM)](https://www.sam.gov) and the
[Federal Awardee Performance and Integrity Information System
(FAPIIS)](https://www.fapiis.gov) have been integrated. This represents core
information for many responsibility determinations and for assessing compliance
with registration requirements. 

### Work in progress

We are integrating historical information on suppliers, reflecting prior
experience performing government contracts based on data from the [Federal
Procurement Data System](https://www.fpds.gov).  Additional, the U.S. Air Force
has a partnership with [Public Spend Forum](https://www.publicspendforum.net),
who has provided us with a mechanism to connect with supplier profiles on their
[GovShop platform](https://govshop.publicspendforum.net). 

### Future Plans

We have numerous ideas for information and analysis that we believe might be
useful to buyers, including supplier risk ratings, past performance
information, public sentiment/news feed data, and automated analysis of
financial statements for public firms (e.g., 10-Ks and other SEC filings).  We
are exploring opportunities and appreciate feedback and ideas.

### Limitations

While in development, we've made the service publicly accessible (the
information that is being presented is compiled entirely from public sources).
The application is subject to potential rate-limiting by upstream servers; if
the prototype sees very heavy usage in a short period then it will,
temporarily, be unable to respond. There are several potential approaches to
address this, however our current focus is on the design and integration of
information.
