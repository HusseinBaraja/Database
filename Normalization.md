# First Normal Form (1NF)
**Definition:** A table is in the First Normal Form if it contains only atomic (indivisible) values and each record is unique.

**Main rule:** no repeating elements or groups of elements.

**Notes:**
- A value that uniquely identifies a row is called a primary key.
- When this value is made up of two or more columns, it is referred to as a concatenated primary key. 

**Rules:**
1. A row of data cannot contain repeating groups of similar data (atomicity) .
2. Each row of data must have a unique identifier (or Primary Key).

**Steps to do:**
1. Fill in empty spaces by replacing null values with default values.
2. Identify the primary key (might be one or two columns).

# Second Normal Form (2NF)
**Definition:** A table is in 2NF if it is in 1NF and all non-key attributes are fully dependent on the primary key. AKA: How a table’s non-key columns (Attributes) relate to the primary key.

**Main rule:** No partial dependencies of non-key columns on a concatenated primary key.
AKA: each non-key attribute in the table must be dependent on the entire primary key.
AKA: Can this column exist without one or the other part of the concatenated primary key? If the answer is "yes" even once, then the table fails Second Normal Form. 

**Examples:**
Primary key                              non-key attribute
1- {Plager_lD, Item_Type} —> {Item_Quantity} ✔ (Fully dependent on composite key)
2- {Plager_lD, Item_Type} —> {Player_Rating} ❌ (Dependent only on Player_ID, not the full key)

On the second one, the player rating attribute is dependent on the player ID only and is not related to the item type, so the player rating attribute is not dependent on the concatenated key ID and Type.

**Notes:**
- A table in 1NF is subject to deletion, update, and insert anomaly.
- We can separate the 1NF table into two different tables that are entirely dependent on their primary key.
- NF2 only applies to tables with a concatenated primary key.

**Rules:**
1. If any column only depends on part of a composite primary key, create a new table for these columns.
2. For a table with a concatenated primary key, each non-primary key column must be examined to determine whether it depends on the full primary key or just a part of it.

**Steps to do:**
1. Identify Composite Primary Keys
2. Analyze every non-primary key column. Determine whether each of these columns depends on the entire primary key or just a part of it.
3. Identify columns that show partial dependency
4. Create a new table. Move columns that have partial dependency to the new table along with the part of the primary key they depend on.
5. Establish the necessary relationships between the new and original tables using foreign keys.



# Third Normal Form (3NF)
Definition: A table is in the Third Normal Form if it is in 2NF and all non-key attributes are not dependent on any other non-key attributes.

**Main rule:** No transitive dependencies.

**Notes:**
- Transitive dependency occurs when a non-key attribute depends on another non-key attribute, which in turn depends on the primary key.
- 3NF ensures that each attribute is directly dependent on the primary key.
- Boyce-Codd Normal Form (BCNF) is a stronger variant of 3NF, often used interchangeably in practical scenarios.

**Example:**
- In a Player table, if `Player_Rating` depends on `Player_Skill_Level` (a non-key attribute) and `Player_Skill_Level` depends on `Player_ID` (the primary key), this creates a transitive dependency.
- To conform to 3NF, remove `Player_Rating` from the Player table and create a separate table linking `Player_Skill_Level` to `Player_Rating`.

**Rules for achieving 3NF:**
1. Identify and remove any transitive dependencies where a non-key attribute depends on another non-key attribute.
2. Create separate tables for attributes that were removed, using the attribute they depend on as a primary key.

**Steps to achieve 3NF:**
1. Analyze each non-key attribute to ensure it depends only on the primary key.
2. Identify transitive dependencies where a non-key attribute depends on another non-key attribute.
3. Remove the dependent non-key attribute from the table.
4. Create a new table where this attribute becomes a primary key or part of it, and link it back to the original table, if necessary, using foreign keys.
