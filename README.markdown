## Introduction

This is a in-memory CQRS Starter kit with the read model built using redux store.

- [nodeCqrs](https://github.com/jamuhl/nodeCQRS) I based my implementation on it.
- [node-eventstore](https://github.com/adrai/node-eventstore) for EventSourcing.

### get it up and running

npm start


### Write side

Using the DDD approach each module should live in a folder inside the domain folder.
Each modules has handlers (mappers) which apply functions like ( aggregateRoot, command) -> [events]
Each modules has reducers which are used to reconstruct the state of the aggregate base on the event stream

### Read side

The read model is a series of reducers


### BDD Tests

The project implements a helper library to test the domain aggregates using a BDD like language.
This implementation was based on [cqrs-starter-kit](https://github.com/edumentab/cqrs-starter-kit) for .NET

The test can expect events:

```
it('Should Return Event Item Created', function() {
    Test(
      given(),
      when({
          command: 'createItem',
          aggId: '123',
          payload:{
            text: 'This is a new Item'
          }
      }),
      then({
          event: 'itemCreated',
          payload:{
            itemId: '123',
            text: 'This is a new Item'
          }
      })
    )
});
```

Or errors:

```
it('Should Give Error', function() {
    Test(
      given(),
      when({
          command: 'changeItem',
          aggId: '123',
          payload:{
            text: 'This is a new Item'
          }
      }),
      thenFailWith(new errors.ItemDoesNotExists())
    )
});
```
