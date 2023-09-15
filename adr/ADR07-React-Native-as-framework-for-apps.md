# ADR07: React Native as framework for apps

## Status

Draft

## Rationale

In a new startup, choosing the right development framework is one of the key factors to success, the decision should take into consideration three main factors: development cost, developer availability, and time-to-market; for those reasons, React Native is our choice due to its popularity and its fit with our projects requirements

## Decision

After weighing the choices we decided to use React Native for our mobile app development, based on those factors:

### Pros of Choosing React Native

- _Works everywhere_: React Native has cross-platform compatibility, allowing us to write code once and deploy it on iOS and Android. This reduces the development time and costs compared to maintaining separate codebases and developers for each platform.
- _Large community and ecosystem_: React Native has a big community of developers, good documentation, and several third-party libraries and plugins. This makes it easier and faster to find solutions to common problems and accelerates development.
- ?? _Native-Like Performance_: React Native uses native components, resulting in close to-native performance, that ensures a smooth and responsive user experience.
- _Code reusability_: Parts of code can be shared between the web, iOS, and Android versions of the app, reducing duplication and simplifying maintenance.
- _Quick development_: React Native familiar architecture speeds up development, enabling developers to reuse UI elements and modules across platforms.
- _Sync between Apps platforms_: DESCRIBE

### Cons of Choosing React Native

- _Limited access to native features_: Even if React Native provides access to some native features, advanced or platform-specific functionalities may require native code integration, increasing complexity.
- _Performance variation_: In general React Native delivers good performance, but some high-demand features can experience performance issues harder to tackle.
- _Learning curve_: Developers new to React Native will require time to get familiar with its concepts, tools, and ecosystem, potentially impacting initial productivity.
- _Dependency on third-party modules_: Relying on third-party libraries and modules can introduce risks related to compatibility, maintenance, and security.
- _Platform updates_: React Native updates may not be aligned with the release schedules of iOS and Android, causing potential compatibility issues.

## Consequences

The decision to use React Native for our mobile app development has the following consequences:

- _Faster development_: We expect a faster development cycle.
- _Cost savings_: Sharing code across platforms, leads to reduced development and maintenance costs compared to the native approach.
- _Potential performance problems_: We need to monitor app performance and have options to optimize/integrate native code if necessary.
- _Learning curve_: the development team will need time to learn its best practices to ensure efficient and faster development.
- _Third-party dependencies_: Manage and vet carefully third-party libraries and modules to avoid potential risks.
- _Smoother user experience_: Focusing on optimizing the user experience instead of coding in multiple platforms, we can deliver better UX/UI for our users.

Choosing React Native aligns with our goal of efficient cross-platform development, but we know the need to monitor the performance and push the learning time for our development team.
