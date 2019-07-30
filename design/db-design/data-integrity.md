# Data Integrity

Some people refer to integrity constraints as business rules. However, business rules is a much broader concept; it includes all of the constraints on the system rather than just the constraints concerning the integrity of the data. In particular, system security — that is, the definition of which users can do what and under what circumstances they can do it —is part of system administration, not data integrity.

**Data integrity** is implemented at several levels of granularity. Domain, transition, and entity constraints define the rules for maintaining the integrity of the individual relations. Referential integrity constraints ensure that necessary relationships between relations are maintained. Database integrity constraints govern the database as a whole, and transaction integrity constraints control the way data is manipulated either within a single database or between multiple databases.

### Data integrity types

* **Domain integrity** — is a rule that defines these legal values \(often implemented as correct _data type_ or _separate table_ with possible values\). Consider whether a domain is permitted to contain unknown or nonexistent values \(_is nullable_\).
* **Transition integrity** — defines the states through which a tuple can validly pass. The status of an entity is usually controlled by a single attribute. In this case, transition integrity can be considered a special type of domain integrity.
* **Entity integrity** — ensures the integrity of the entities being modeled by the system. At the simplest level, the existence of a _primary key_ is an entity constraint that enforces the rule "every entity must be uniquely identifiable". Entity constraints can also effect multiple attributes \(_compound unique constraints_\). Be careful of multiple-attribute constraints; they might indicate that your data model isn't fully normalized.
* **Referential integrity** — implements the links between relations \(_foreign keys_\).
* **Database integrity** — references more than one relation: "A Customer is not allowed to have a status of 'Preferred' unless he or she has made a purchase in the last 12 months". Can be implemented anywhere: from procedures on database side to checks on front-end side.
* **Transaction integrity** — constraints govern the ways in which the database can be manipulated. A transaction is usually defined as a "logical unit of work".

