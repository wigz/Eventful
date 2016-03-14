# Eventful
A simple pub/sub superclass for ES2015. Allows you to use events to communicate between instances.

Use
---

```javascript
class SomeOtherEventfulClass extends Eventful {

  /*
  ------------------------------------------
  | constructor:void
  |
  | init:object - init params
  |
  | Construct.
  ------------------------------------------ */
  constructor(init) {
    super();

    // trigger
    this.trigger('another_event', {'data': 'another data'});
  }
}

class MyClass extends Eventful {

  /*
  ------------------------------------------
  | constructor:void
  |
  | init:object - init params
  |
  | Construct.
  ------------------------------------------ */
  constructor(init) {
    super();

    let my_instance = new SomeOtherEventfulClass();

    // use internal
    this.on('some_event', this.onSomeEvent);

    // use external
    my_instance.on('another_event', (e) => this.onAnotherEvent(e));

    // trigger
    this.trigger('some_event', {'data': 'some data'});

    // trigger here
    my_instance.trigger('another_event', {'data': 'another data'});

    // remove specific
    this.off('some_event', this.onSomeEvent);

    // remove all
    my_instance.off('another_event');
  }

  /*
  ------------------------------------------
  | onSomeEvent:void
  |
  | e:object - event object
  |
  | Handle some_event.
  ------------------------------------------ */
  onSomeEvent(e) {
    console.log(e);
  }

  /*
  ------------------------------------------
  | onAnotherEvent:void
  |
  | e:object - event object
  |
  | Handle another_event.
  ------------------------------------------ */
  onAnotherEvent(e) {
    console.log(e);
  }
}
```
