This man is about databases
> Sources :
> Hussein Nasser " Relational Databases ACID Transactions (Explained by Example) " Video

# Types

## Relational

## NoSQL

This architecture relaxes some of the ACID requirement specifically the `Consistency` propriety to the benefit of scalability and performance. The funny thing is that they are marketed as " Eventually Consistent " which is joke in my point of view since this means that if you wait long enough you're going to get the data you are looking for meaning if the user wants to see the real database value he is supposed to keep updating the page (reading) until he gets a new value which might have been already overwritten by a new one.

# ACID

These are the bases of a "Relational" database

- Atomicity
- Consistency
- Isolation
- Durability

## Transaction

A transaction is a bunch of quires to the database meant to do a full action. For Example Substituting 10$ from account `A` with 100$ and adding them to account `B` with 10$ , this transaction does two things `quires` to the database

- A=100-10
- B=10+10

## Atomicity

This means that a transaction is going to happen successfully or not at all. Like out previous example if the first query is executed and the database crashes for some reason then the database will end in a state where

- A=90
- B=10

Which is obviously not good since we've lost 10$ with no way to `Rollback` the transaction.

With Atomic transaction this wouldn't have happened since if the transaction is not fully committed it will never succeed in the first place.

## Consistency

Is a propriety that emerges form having other proprieties.

### Consistency in Data



### Consistency in Reads

It generally reads Inconsistency occurs when multiple database servers are clustered together, this happens due to network latency and other variables resulting in out of date reads in some cases.

## Isolation

Is the ability of an `Inflight` transactions to see each other's changes, `Inflight` means under processing

### Read Phenomena

These are some read issues a transaction might encounter due to various isolation issues

- Dirty Reads
- Non-repeatable Reads
- Phantom Reads
- Lost Updates

#### Dirty Read

A transaction is reading data that haven't been committed yet I.E it's still in memory and can be `Rolledback`, this may cause a contradiction if the first query read the old data while the second one read the dirty one.


#### Non-repeatable Read

The same as `Dirty Read` applies here with the difference that the transaction is actually committed or synced, which also leads to conflicts in readings.

#### Phantom Read

This type as far as I can tell is reading data that wasn't there in the first transaction's query but showed up in the second query making results inconsistent.

#### Lost Updates



### Isolation Levels

So what are the fixes to all these reading issues. And if you haven't noticed yet the answer is `Isolation`, Which can be in four different levels.

> Note : The database performance goes down with each level down, of course at the benefit of more Isolation

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable

#### Read Uncommitted

Is basically no isolation, meaning all changes are visible to all transactions. All reading issues are present here.

#### Read Committed

Transaction queries are allowed to only see committed data at the time of each query. (realtimeish)

#### Repeatable Read

Transaction queries are allowed to see committed queries at the beginning of the transaction it self. It's a kind of a snapshot of the database for each transaction when it starts, Or a write lock on the database until the transaction is done. (asyncish)

#### Serializable

All transactions are processed in a queue one after the other which means at any given time only and only one transaction is accessing the database for read or write. In this case it's obvious that the performance is not a concern at all for example " Banking, Military ... " .

#### Summary Table

|---------------------|-------------|---------------------|---------------|--------------|
| Read Phenomena >    |             |                     |               |              |
| ------------------- | Dirty Reads | Non-Repatable Reads | Phantom Reads | Lost Updates |
| Isolation Level v   |             |                     |               |              |
|---------------------|-------------|---------------------|---------------|--------------|
| Read Uncommitted    | yes         | yes                 | yes           | yes          |
|---------------------|-------------|---------------------|---------------|--------------|
| Read Committed      | no          | yes                 | yes           | yes          |
|---------------------|-------------|---------------------|---------------|--------------|
| Repatable Read      | no          | no                  | yes           | no           |
|---------------------|-------------|---------------------|---------------|--------------|
| Serializable        | no          | no                  | no            | no           |
|---------------------|-------------|---------------------|---------------|--------------|

## Durability

Means The data stays in the database no matter what until eventually updated or deleted. This means the data must be stored in a non-volatile storage media that is error free.

An example of a Non-Durable databased is `Redis` & `Memcachd` due to the fact that they are In-Memory database desigen for extremly fast processing.


# Indexing


