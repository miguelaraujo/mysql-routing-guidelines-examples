# MySQL Routing Guidelines – Examples

This repository contains **practical examples of MySQL Routing Guidelines**, illustrating how to design and reason about query routing policies for modern MySQL architectures.

These guidelines are meant to be **read, adapted, and extended**, not copied blindly.

---

## What are Routing Guidelines?

MySQL Routing Guidelines provide a **declarative framework** to control how client sessions are routed by MySQL Router.

They allow you to:

- Express **routing intent** explicitly, rather than relying on implicit read/write behavior
- Enable **smarter routing** through dynamic, flexible, and declarative routing policies
- **Isolate workloads** safely to protect latency-sensitive OLTP traffic
- Encode **explicit trade-offs** between availability and predictability
- Build **future-ready architectures** that scale across complex and evolving topologies
- etc.

Routing Guidelines are evaluated dynamically by MySQL Router and are independent of application logic.

Routing Guidelines are defined and managed using **MySQL Shell and AdminAPI**, and stored centrally as part of the topology metadata.


---

## Examples in this repository

### `fosdem26.json`
A complete Routing Guideline built step by step during the *“MySQL Routing Guidelines: Designing Smarter Query Routing Together”* session at the pre-FOSDEM MySQL Belgian Days 2026.

**Scenario covered:**
- Latency-sensitive OLTP workload
- Dedicated read replicas for:
  - Backups
  - Analytics
  - Reporting
- Strict routing by default
- Explicit, opt-in degradation when preferred replicas are unavailable

This example demonstrates:
- Destination classes based on server role and tags
- Routing decisions driven by session intent (schema, connection attributes)
- Controlled fallback behavior without compromising OLTP predictability

More examples may be added over time.

---

## How to use an example

Load a guideline using MySQL Shell and AdminAPI:

```py
\connect clusteradmin@host

// Get the Cluster object
cluster = dba.get_cluster()

// Import the routing guideline from the JSON file
cluster.import_routing_guideline("fosdem26.json")
```

## Further reading

For more background and technical details on MySQL Routing Guidelines, see:

- [Smarter Query Routing with MySQL Routing Guidelines](https://dev.mysql.com/blog-archive/smarter-query-routing-with-mysql-routing-guidelines/)
- [MySQL Routing Guidelines: A Practical Guide to Management and Configuration](https://blogs.oracle.com/mysql/mysql-routing-guidelines-a-practical-guide-to-management-and-configuration)
- [MySQL Routing Guidelines: Breaking Down the Mechanics in MySQL Router](https://blogs.oracle.com/mysql/mysql-routing-guidelines-breaking-down-the-mechanics-in-mysql-router)
