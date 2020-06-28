# SQL

## Database design

[Conceptual database design](https://cheatography.com/natalie-moore/cheat-sheets/conceptual-database-design)

### Constraint (PostgreSQL)
- [Check Constraint](https://www.w3resource.com/PostgreSQL/check.php)
- [Not Null Constraint](https://www.w3resource.com/PostgreSQL/not-null.php)
- [Unique Constraint](https://www.w3resource.com/PostgreSQL/unique.php)
- [Primary Key Constraint](https://www.w3resource.com/PostgreSQL/primary-key-constraint.php)
- [Foreign Key Constraint](https://www.w3resource.com/PostgreSQL/foreign-key-constraint.php)

### [Trigger](https://www.w3resource.com/PostgreSQL/postgresql-triggers.php) (PostgreSQL)

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

### [Composite/Surrogate Key?](https://asktom.oracle.com/pls/apex/f?p=100:11:0%3A%3A%3A%3AP11_QUESTION_ID:580828234131) 

- a sequence is smaller then 3 columns will be. If the key of this table is a foreign key in lots of other tables -- the space savings can be enourmous.

- people frequently try to update a primary key to correct data -- using a surrogate key which is imutable solves forever this update cascade problem as you never update the primary key (the sequence) you update the 3 columns which are not stored anywhere.

- it is easier to code :

```
select * from p, c where p.primary_key = c.foreign_key
```
then
```
select * from p, c where p.id1 = c.fk1 and p.id2 = c.fk2 and p.id3 = c.fk3
```
and the first query runs faster.

- Those are the things I said to take into consideration. As I said -- if the composite primary key is not a foreign key in lots of tables -- go for the composite primary key. 
- If it is -- give serious consideration to the surrogate key populated via a sequence (and don't even consider that "gaps" might be there -- that is not even a little bit relevant, it is just a unique id).