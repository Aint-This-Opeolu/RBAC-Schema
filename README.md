# RBAC Schema

This project provides a **Role-Based Access Control (RBAC) schema** built on PostgreSQL. It defines the core entities—principals, roles, permissions, teams, and access requests—needed to manage fine-grained authorization in modern systems.

The schema includes:
- **Principals**: Users or services requesting access.
- **Roles**: Bundled permissions defining allowed actions.
- **Role Bindings**: Assignments connecting principals to roles for specific resources.
- **Access Requests**: Temporary elevation workflows for just-in-time access.
- **Audit Logs**: Complete traceability of access changes and decisions.

The project comes preloaded with **mock data** for testing and exploration, so you can see how the RBAC flows work out of the box.

---

## Getting Started

To get this running locally, follow these steps:


# 1. Run PostgreSQL with Docker
docker run --name postgres \
  -e POSTGRES_USER=<YourName> \
  -e POSTGRES_PASSWORD=<YourPassword> \
  -e POSTGRES_DB=postgres \
  -p 5432:5432 \
  -d postgres

# 2. Apply the Schema
Get-Content "C:\path\to\schema.sql" | docker exec -i postgres psql -U <YourName> -d postgres

# 3. Verify Data
docker exec -it postgres psql -U <YourName> -d postgres

# Inside psql, run:
\dt
select * from principals;
select * from roles;

# 4. Example Access Request
insert into access_requests (principal_id, role_id, resource_path, reason, requested_duration, status) values
((select id from principals where username = 'test-user'),
 (select id from roles where name = 'sre'),
 'acme:payments:prod:cloud.vm:database-server',
 'Emergency database maintenance required',
 interval '2 hours',
 'pending');



Remember, chat 
All these things use mock data!!!!
You can edit it to fit the different roles in your own organization.
