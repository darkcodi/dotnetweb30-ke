# Sessions, transactions, locks

### Sessions

When a client application establishes a connection to an RDBMS server, it is said that it opens a session. The session becomes this application's private communication channel.

The user of the application may change some preferences within the session \(for example, default language or default date format\); these settings would affect only the session environment and remain valid only for the duration of the session.

| SET Statement | Description |
| :--- | :--- |
| SET ANSI\_DEFAULTS {ON \| OFF} | Specifies that all the defaults used for the duration of the session should be these of ANSI defaults. This option is provided for compatibility with SQL Server 6.5 or later |
| SET ANSI\_NULL\_DFLT\_OFF {ON \| OFF} | Specifies whether columns could contain NULL value by default. If set to ON, the new columns created would allow NULL values \(unless NOT NULL is specified\); otherwise it would raise an error. It has no effect on the columns explicitly set for NULL. It is used to override default nullability of new columns when the ANSI null default option for the database is TRUE. |
| SET ANSI\_NULL\_DFLT\_ON {ON \| OFF} | Essentially, the same as the statement above, with one exception: it is used to override default nullability of new columns when the ANSI null default option for the database is FALSE. |
| SET ANSI\_NULLS {ON \| OFF} | Specifies the SQL-92 compliant behavior when comparing values using operators EQUAL \(=\) and NOT EQUAL \(&lt; &gt;\). |
| SET ANSI\_PADDING {ON \| OFF} | Specifies how the values that are shorter than the column size for CHAR, VARCHAR, BINARY, and VARBINARY data types are displayed. |
| SET ANSI\_WARNINGS {ON \| OFF} | Specifies whether a warning should be issued when any of the following conditions occur: presence of NULL values in the columns evaluated in the aggregate functions \(like SUM, AVG,COUNT, etc.\); divide-by-zero and arithmetic overflow errors generate an error message and the statement rolls back when this option is set to ON; specifying OFF would cause a NULL value to be returned in the case. |
| SET DATEFORMAT {&lt;format&gt; \| @&lt;format ID&gt;} | Specifies the order of the date parts for DATETIME and SMALLDATETIME input |
| SET CONCAT\_NULL\_YIELDS\_NULL {ON \| OFF} | Specifies what would be the result of concatenation of the column values \(or expressions\) should any or both of them contain NULL. |
| SET LANGUAGE { &lt;language&gt; \| @&lt;language ID&gt;} | Specifies the default language for the session. This setting affects the datetime format, and system messages returned by SQL Server. |
| SET NOCOUNT {ON \| OFF} | SQL Server usually returns a message indicating how many rows were affected by any given statement. Issuing this command would stop this message. |
| SET NUMERIC\_ROUNDABORT {ON \| OFF} | Specifies the severity of an error that results in loss of precision; if set to OFF the rounding generates no error; when it is set to ON, then an error will be generated and no results returned. Depending on some other settings, a NULL might be returned. |
| SET ROWCOUNT &lt;integer&gt; | If this statement is used, Microsoft SQL Server stops processing a query after the required number of rows \(specified in the SET statement\) is returned. |

#### Example

```sql
SET NOCOUNT, ANSI_DEFAULTS ON
```

### Transactions

{% hint style="success" %}
A transaction is one of the mechanisms provided within SQL to enforce **database integrity** and maintain **data consistency**.
{% endhint %}

A transaction complements the concept of the session with additional granularity — it divides every operation that occurs within the session into logical units of work.

In this way, database operations — those involving data and structure modifications — are performed step-by-step and can be rolled back at any time, or committed if every step is successful.

#### ACID

A transaction must pass the ACID test:

* **Atomicity.** Either all the changes are made or none.
* **Consistency.** All the data involved into an operation must be left in a consistent state upon completion or rollback of the transaction; database integrity cannot be compromised.
* **Isolation.** One transaction should not be aware of the modifications made to the data by any other transaction unless it was committed to the database. Different isolation levels can be set to modify this default behavior.
* **Durability.** The results of a transaction that has been successfully committed to the database remain there.

![](../../.gitbook/assets/image%20%28154%29.png)

The transaction model, as it is defined in the ANSI/ISO standard, utilizes the implicit start of a transaction, with an explicit **COMMIT**, in the case of successful execution of all transactions logical units, or an explicit **ROLLBACK**, when the noncommitted changes need to be rolled back.

No changes are taking place until the last COMMIT is executed.

#### Example

```sql
BEGIN TRAN
SELECT * FROM customer
UPDATE customer SET cust_status_s = 'N'
COMMIT TRAN
```

{% hint style="warning" %}
Integrity = strong types, no illegal values as determined by the data model & constraints, foriegn keys, unique constraints and stuff like that.
{% endhint %}

{% hint style="warning" %}
Consistency = being able to read only committed data a given point in time, not the intermediate steps. The data value stored in the database must satisfy certain consistency constraints.
{% endhint %}

### Locks

Concurrency is one of the major concerns in a multiuser environment. Locks are used to solve concurrency problems.

There are two broad categories of concurrency:

* **Optimistic.** Transactions with optimistic concurrency work on the assumption that resource conflicts. Optimistic transactions check for potential conflicts when committing changes to a database and conflicts are resolved by resubmitting data.
* **Pessimistic.** Pessimistic transactions expect conflicts from the very beginning and lock all resources they intend to use.

Locks are used to implement pessimistic transactions.

#### Lock modes

| Lock Mode | Description |
| :--- | :--- |
| SHARED \(S\) | This type of lock is used for read-only operations. |
| UPDATE \(U\) | This lock is used whenever the data is updated. |
| EXCLUSIVE \(X\) | Prevents all other transactions from performing UPDATE, DELETE or INSERT. |
| INTENT | This is used to establish a hierarchy of locking: intent, shared intent, exclusive, and shared with intent exclusive. An intent lock indicates that SQL Server wants to acquire a shared or exclusive lock on some resources down in the hierarchy \(e.g., table — page — row\); at the very least the intent lock prevents any transactions from acquiring an exclusive lock on the resource. |
| SCHEMA | This lock type is used when a DDL operation is performed. |
| BULK UPDATE \(BU\) | These locks are used when bulk copying is taking place. |

#### Lock hints

The lock mode is either selected by the SQL Server itself, or based on the type of operation performed. To manually specify the locking mode, one should use the table-level locking hints that fall into one of the categories listed below.

| Locking Hint | Description |
| :--- | :--- |
| NOLOCK | This hint issued in a SELECT statement specifies that no shared locks should be used and no exclusive locks should be honored; this means that the SELECT statement could potentially read uncommitted transactions \(dirty reads\). |
| UPDLOCK | Instructs SQL Server to use UPDATE locking \(as opposed to shared locks\) while reading data; makes sure that data has not changed if an UPDATE statement follows next. |
| XLOCK | Places an exclusive lock until the end of a transaction on all data affected by the transaction. Additional levels of granularity can be specified with this lock. |
| ROWLOCK | Specifically instructs SQL Server to use row-level locks \(as opposed to page and table-level\). |

#### Deadlocks

The classic deadlock situation arises when two \(or more\) sessions are waiting to acquire a lock on a shared resource, and none of them can proceed because a second session also has a lock on some other resource that is required by the first session.

Usually RDBMS resolves situations like this automatically by killing one of the processes and rolling back all the changes it may have made.

It is possible to volunteer a session to become a deadlock victim by setting the DEADLOCK\_PRIORITY parameter within that session.

```sql
SET DEADLOCK_PRIORITY LOW
```

