# ADR07: FrontEnd

## Status

Proposed

## Rationale

An important thing for startups is being as efficient with the money as possible. In terms of front-end that is: sharing and reusing as much of the UI as possible across supported platforms Android, iOS, Web Cross-platform, and hybrid frameworks are the best tools for the job, offering high code reuse.

## Decision

Our decision is ReactNative. It's based on a popular web framework, React. React will be used for the web, whereas ReactNative will be used for mobile apps. ReactNative can be used for building web apps but going that way implies many, often bad, compromises that may result in unintended and tedious work of separating mobile and web apps.

## Pros

- **Single team**: A single front-end team will be able to build UI for all platforms, lowering cost and time-to-market.
- **Code reuse**: Business logic and most of the UI is reusable which drastically lowers costs and time to market.
- **Mature community**: ReactNative is a popular framework and it was the go-to framework for a long time, resulting in a reach library pool.
- **Fast development**: ReactNative is popular for its fast development when it comes to the UI, emphasizing hot-reload among other things.

## Cons

- **Non-native performance**: ReactNative doesn't offer native performances due to its binding to native components mechanism.
- **Limited native features use**: ReactNative is not a native app and even tho it has a lot of libraries, it doesn't have access to all native features.
- **Use of third-party modules**: Third-party modules can suffer from problems such as compatibility, security, updates, support for the latest features, etc.
- **Platform updates**: ReactNative doesn't automatically get the latest OS features, which are available to native apps.

## Consequences

- **Cost and time saving**: Having a single team that will reuse most of the work drastically lowers cost and time-to-market.
- **Potential performance issues**: The app has to be well tested for potential bad performance.
- **Not up to date with latest OS features**: This shouldn't be much of a problem since we need limited access to native features.
- **Vet third-party modules**: The team should be careful and vet for modules with good support and reputation.
