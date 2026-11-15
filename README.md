# bysellens-product-db

> product bounded context: database (schema, seeds, migrations)

Part of the **LMS Library** distributed system — team `lms-library`, Grupo 2.
Governance and documentation live in [`library-docs`](https://github.com/code-corhuila/library-docs).

## Branching

Three permanent branches. **None of them accepts a direct commit** — you enter through a child
branch and leave through a Pull Request.

```
develop  <--PR--  feat/... fix/... chore/...
qa       <--PR--  qa/...
main     <--PR--  release/...  hotfix/...
```

Promotion happens **by re-application** (`git cherry-pick -x`), never by merging one permanent
branch into another: `merge develop -> qa` and `merge qa -> main` do not exist in this model.

`main` requires **1 approval from `ariel5253`**. On `develop` and `qa` the team sets its own review
rule.

Full policy: `00-governance/branching-policy.md` in `library-docs`.

## Database

Product uses PostgreSQL. The service connects to the `product` schema and manages its schema
with Flyway; Hibernate validates the mapped schema at startup. The initial migration is
[`db/migration/V1__initial.sql`](db/migration/V1__initial.sql).

The migration creates the `productos` table, its constraints, and an index on `activo`.
No seed data is included. Configure database connection details through the service's
environment; credentials and database backups do not belong in this repository.
