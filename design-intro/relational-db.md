`ACID` - a transaction in a database that has 4 properties

`Atomicity` - if a transaction consists of multiple sub-operations, the operations will be considered a unit

`Consistency` - any transaction in a db will conform to the rules of the db

`Isolation` - multiple transactions will be done in a queue

`Durability` - the effects of transactions will be permanent

Database Index

- Create an auxiliary ds that will be used for faster searching
- How does it do it?
  - ordered in a sorted order

```SQL
BEGIN TRANSACTION;
UPDATE balances SET balance = balance - 100 WHERE username = 'david';
UPDATE balances SET balance = balance + 100 WHERE username = 'mary';
COMMIT;
```
