# Relationships \(One-to-One, One-to-Many\)

At the conceptual level, _relationships_ are simply associations between entities. The statement "Customers buy products" indicates that a relationship exists between the entities Customers and Products. The entities involved in a relationship are called its _participants_. The number of participants is the _degree_ of the relationship. \(The degree of a relationship is similar to, but not the same as, the degree of a relation, which is the number of attributes.\)

The relationship between any two entities can be one-to-one, one-to-many, or many-to-many. **One-to-one relationships** are rare, most often being used between supertype and subtype entities.

**One-to-many relationships** are probably the most common type. An invoice includes many products. A salesperson creates many invoices. These are both examples of one-to-many relationships.

Although not as common as one-to-many relationships, **many-to-many relationships** are also not unusual and examples abound. Customers buy many products, and products are bought by many customers. Teachers teach many students, and students are taught by many teachers. Many-to-many relationships can't be directly implemented in the relational model, but their indirect implementation is quite straightforward – just create an another table, which contains relations.

