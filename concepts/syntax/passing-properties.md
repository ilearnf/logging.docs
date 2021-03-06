# Providing property values

There are three supported ways to pass property values for placeholders in [message template](message-templates.md) when using [logging extensions](logging-extensions.md).



### 1. Pass property values as optional object arguments:

```csharp
log.Info("Welcome, {User}. You have {UnreadCount} unread messages.", "Jenny", 2);
```

Property names are inferred from placeholders in message template. 

If arguments count exceeds template placeholders count, excess arguments are named with numbers denoting their positions:

```csharp
log.Info("Welcome, {User}.", "Jenny", "foo", "bar");
// produced event properties: {"User": "Jenny", "1": "foo", "2": "bar"}
```

If provided arguments count is not sufficient to account for all template placeholders, the names for existing arguments are still inferred.

{% hint style="info" %}
Strictly speaking, this approach does not support multiple occurences of the same placeholder name within a message template \(last matched argument wins\):

```csharp
log.Info("Welcome, {name}. {name}, you have {count} unread messages.", 
    "Jenny", 10);
// The result is: "Welcome, 10. 10, you have  unread messages."
```

Although it's safe to use if all duplicate placeholder occurences in the template are located far enough not to get matched to any arguments:

```csharp
log.Info("Welcome, {name}. You have {count} unread messages, {name}.",
    "Jenny", 10);
// The result is: Welcome, Jenny. You have 10 unread messages, Jenny.
```
{% endhint %}

### 

### 2. Use a single object with named properties:

```csharp
 log.Info("Welcome, {User}. You have {UnreadCount} unread messages.", 
     new {User = "Jenny", UnreadCount = 2});
```

When using this syntax, user is responsible for making sure that object property names match the names of placeholders in message template.



### 3. Use positional placeholders:

```csharp
log.Info("Welcome, {0}. You have {1} unread messages.", "Jenny", 2);
```

Despite being somewhat deprecated nowadays, this syntax enables gradual migration from libraries that do not support structured logging.

It also supports multiple occurences of the same placeholder within a single template:

```csharp
log.Info("Welcome, {0}. {0}, you have {1} unread messages.", "Jenny", 2);
```

