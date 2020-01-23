# Filtering events

**Prerequisites**:

* Install [abstractions module](../modules/abstractions.md)
* Read about general log [configuration practices](../configuration.md)
* Read about [log interface](../concepts/log-interface.md)
* Read about [log events](../concepts/log-events.md)

Filtering allows a particular `ILog` instance to only record a subset of incoming log events. Events can be filtered by level, properties or literally any other information present.

### Filter by level

Set a minimum allowed log level \(events of lower levels will be dropped\):

```csharp
log = log.WithMinimumLevel(LogLevel.Warn);
```

Selectively disable some log levels:

```csharp
log = log.WithDisabledLevels(LogLevel.Debug, LogLevel.Fatal);
```



### Filter by a single property

Select events having a property with given name and a of given type value satisfying a predicate:

```csharp
log = log.WithEventsSelectedByProperty<string>("prop", value => value == "foo");
```

Drop events having a property with given name and a value of given type satisfying a predicate:

```csharp
log = log.WithEventsDroppedByProperty<string>("prop", value => value == "foo");
```



### Filter by all properties

Select events whose properties dictionary satisfies given predicate:

```csharp
log = log.WithEventsSelectedByProperties(props => props.ContainsKey("prop"));
```

Drop events whose properties dictionary satisfies given predicate:

```csharp
log = log.WithEventsDroppedByProperties(props => props.ContainsKey("prop"));
```



### Filter by source context

Select events having a source context with given value \(values are case-sensitive\):

```csharp
log = log.WithEventsSelectedBySourceContext("foo");

log.ForContext("foo").Info("Hello!"); // will be logged
log.ForContext("bar").Info("Hello!"); // will not be logged
```

Drop events having a source context with given value \(values are case-sensitive\):

```csharp
log = log.WithEventsDroppedBySourceContext("foo");

log.ForContext("foo").Info("Hello!"); // will not be logged
log.ForContext("bar").Info("Hello!"); // will be logged
```

Drop events below some level having a source context with given value \(values are case-sensitive\):

```csharp
log = log.WithMinimumLevelForSourceContext("foo", LogLevel.Warn);

log.ForContext("foo").Info("Hello!"); // will not be logged
log.ForContext("foo").Warn("Hello!"); // will be logged
```

There's also an alternative syntax that allows to infer context values from type names:

```csharp
log = log.WithEventsSelectedBySourceContext<FooClass>();
log = log.WithEventsDroppedBySourceContext<FooClass>();
log = log.WithMinimumLevelForSourceContext<FooClass>(LogLevel.Warn);
```



### Filter by arbitrary event content

Select events satisfying given predicate:

```csharp
log = log.SelectEvents(@event => @event.Exception == null);
```

Drop events satisfying given predicate:

```csharp
log.DropEvents(@event => @event.Exception == null);
```

