---
layout: post97
title:  Space Persistency
categories: XAP97
parent: programmers-guide.html
weight: 700
---

{%wbr%}


{% section %}
{% column  width=10% %}
![space-document.png](/attachment_files/subject/persistence.png)
{% endcolumn %}

{% column width=90% %}
XAP provides advanced persistency capabilities for the space architecture.
{% endcolumn %}
{% endsection %}

<hr/>


- [Overview](./space-persistency.html){%wbr%}
XAP persistency overview.

- [Direct persistence](./direct-persistency.html){%wbr%}
Direct persistency mode support Read-Write Through

- [Hibernate integration](./hibernate-space-persistency.html){%wbr%}
The default Hibernate implementation of the Space Persistency APIs.

- [Space Data Source API](./space-data-source-api.html){%wbr%}
The space Data Source API is used for reading data and meta data from the data source.

- [Space Synchronization Endpoint API](./space-synchronization-endpoint-api.html){%wbr%}
The space synchronization endpoint API is used for synchronizing data from the space to an external application or a data base.

- [Initial Load](./space-persistency-initial-load.html){%wbr%}
Space data source initial Load pre-loads the space with data before it is available for clients.

- [Asynchronous Persistence](./asynchronous-persistency-with-the-mirror.html){%wbr%}
Reliable Asynchronous Persistency (Mirror)

- [Transient Entries](./transient-entries.html){%wbr%}
How to specify that some objects in a persistent space should not be saved to the persistent storage.

- [Advanced Concepts](./space-persistency-advanced-topics.html){%wbr%}
Space Persistency advanced topics such as advanced operations, tuning, troubleshooting, and limitations.

- [Migrating Hibernate](./persistency-migrating-hibernate.html){%wbr%}
XAP’s persistency approach consists of several paradigms for data persistency, according to the application needs. This section gives a basic overview of each paradigm.

- [Migrating External Data Source](./migrating-from-external-data-source-api.html){%wbr%}
This page describes how EDS implementations prior to GigaSpaces version 9.5 should migrate to the new Space Persistency APIs.

- [Second Level Hibernate Cache](./gigaspaces-for-hibernate-orm-users.html){%wbr%}
Using XAP as a Hibernate cache provider; creating a Hibernate-integrated Data Grid with your existing ORM.
<hr/>


