# Home

## Vostok.Logging in a nutshell

Vostok.Logging is a [set](modules/) of libraries providing structured logging for .NET applications, much like [Serilog](https://serilog.net/), but tightly integrated into Vostok ecosystem.

## Guiding design principles

* **Logging system should not be able to significantly impact application health or performance.**

  * [Guarantees](guarantees.md) section covers this topic in greater detail.

* **Configuration is done in code**.

  * Configuring and composing loggers in code is preferable to clumsy XML files. See [Configuration](configuration.md) section for an in-depth discussion.

* **Extensibility is valued.**

  * The libraries are designed in a way that encourages creating custom implementations of logs and decorators.

* **Performance is of essence.**
  * Implementations go to great lengths to provide a throughput level sufficient for applications handling tens or even hundreds of thousands of requests per second.

## Features

* **Structured logging**

  * [Log events](concepts/log-events.md) contain key-value properties which are later used for querying the log data or rendering it to text.

* **Reliable built-in log implementations**

  * [Console](implementations/console-log.md), [file](implementations/file-log.md) and [Hercules](implementations/hercules-log.md) logs comply to strict [guarantees](guarantees.md) and offer solid performance.

* **Easy configuration**

  * Most log implementations require just one line of code to set up \(see [Quickstart](quick-start.md)\).

* **Customizable formatting**

  * Output produced by text-based logs \([console](implementations/console-log.md) and [file](implementations/file-log.md)\) can be customized with [output templates](concepts/formatting/output-templates.md).

* **Filtering of log events**

  * There's built-in support for [filtering](how-to-guides/filtering-events-by-level.md) by level, properties or arbitrary contents of [log events](concepts/log-events.md).

* **Enrichment of log events with custom properties**

  * Log events can be dynamically [enriched](how-to-guides/enriching-events-with-custom-properties.md) with new properties either specified by user or provided from ambient context.

* **Support for contextual information tied to log events**

  * Explore the [source](concepts/source-context.md) and [operation](concepts/operation-context.md) context sections to learn more.

* **Integrations with other popular logging libraries**

  * There are adapters available for [Serilog](integrations/serilog.md), [log4net](integrations/log4net.md) and [Microsoft.Extensions.Logging](integrations/microsoft-logging.md).

## Good starting points

{% page-ref page="quick-start.md" %}

{% page-ref page="modules/" %}

{% page-ref page="concepts/log-interface.md" %}

{% page-ref page="concepts/log-events.md" %}

{% page-ref page="concepts/syntax/" %}

