# SQL

## Database design

[Conceptual database design](https://cheatography.com/natalie-moore/cheat-sheets/conceptual-database-design)

#### Constraint (PostgreSQL)
- [Check Constraint](https://www.w3resource.com/PostgreSQL/check.php)
- [Not Null Constraint](https://www.w3resource.com/PostgreSQL/not-null.php)
- [Unique Constraint](https://www.w3resource.com/PostgreSQL/unique.php)
- [Primary Key Constraint](https://www.w3resource.com/PostgreSQL/primary-key-constraint.php)
- [Foreign Key Constraint](https://www.w3resource.com/PostgreSQL/foreign-key-constraint.php)

#### [Trigger](https://www.w3resource.com/PostgreSQL/postgresql-triggers.php) (PostgreSQL)

Uses for triggers:

- Enforce business rules
- Validate input data
- Query from other files for cross-referencing purposes
- Generate a unique value for a newly-inserted row in a different file.
- Write to other files for audit trail purposes
- Replicate data to different files to achieve data consistency
- Access system functions

Benefits of using triggers in business:

- Global enforcement of business rules. Define a trigger once and then reuse it for any application that uses the database.
- Easier maintenance. If a business policy changes, you need to change only the corresponding trigger program instead of each application program.
- Faster application development. Because the database stores triggers, you do not have to code the trigger actions into each database application.
- Improve performance in client/server environment. All rules run on the server before the result returns.