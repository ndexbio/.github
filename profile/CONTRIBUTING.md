NDEx (the Network Data Exchange) is an open source ecosystem for storing, sharing, and publishing biological networks. It is developed as a family of projects — a REST server and data model, client libraries in several languages, web applications, and a collection of analysis and search services — and it welcomes contributions from the community. Whether you're fixing a bug, adding a feature, improving documentation, or helping others, your contributions are appreciated.

This document covers general guidelines that apply across the ecosystem. Each project also has its own README and, in some cases, its own contributing notes with project-specific details — please read the relevant one before starting work.

## Projects

The NDEx ecosystem lives under the [`ndexbio` GitHub organization](https://github.com/ndexbio). The most commonly contributed-to projects are:

**Core server and data model**
- [`ndex-rest`](https://github.com/ndexbio/ndex-rest) — the NDEx REST server (Java).
- [`ndex-object-model`](https://github.com/ndexbio/ndex-object-model) — the Java object model for the NDEx external data model, shared by applications that access NDEx via the API.
- [`openapi-specification`](https://github.com/ndexbio/openapi-specification) — the OpenAPI specification for the NDEx REST API.

**Web applications and front ends**
- [`ndex3`](https://github.com/ndexbio/ndex3) — the current NDEx web application (TypeScript / Next.js).
- [`iquery`](https://github.com/ndexbio/iquery) — the front end for the NDEx Integrated Query search portal (JavaScript).

**Client libraries**
- [`ndex2-client`](https://github.com/ndexbio/ndex2-client) — the NDEx2 client for Python.
- [`ndex-js-client`](https://github.com/ndexbio/ndex-js-client) — the JavaScript client library.
- [`ndex-java-client`](https://github.com/ndexbio/ndex-java-client) — the Java client library.

**Services**
- Search, enrichment, and query services such as [`ndexsearch-rest`](https://github.com/ndexbio/ndexsearch-rest), [`ndex-enrichment-rest`](https://github.com/ndexbio/ndex-enrichment-rest), [`ndex-interactome-search`](https://github.com/ndexbio/ndex-interactome-search), and [`ndex-neighborhood-query-java`](https://github.com/ndexbio/ndex-neighborhood-query-java).

If you're not sure which repository owns the code you want to change, open an issue on the project you think is closest and the maintainers will help route it.

## Getting Started

New contributors unsure about what to work on can explore a project's open issues, especially any tagged `help-wanted` or `good-first-issue`. Original ideas are also welcome — the best place to float them is the [GitHub Discussions](https://github.com/orgs/ndexbio/discussions) or the relevant project's issue tracker, so maintainers can help shape the approach before you invest time in code.

If you have a question about using NDEx rather than developing it, the public NDEx server and its documentation at [ndexbio.org](https://www.ndexbio.org) are often the fastest place to find an answer.

## Submitting Issues

Before writing code, file a short, descriptive issue on the relevant project's issue tracker. A good issue clearly describes the bug or the feature being proposed, and for bugs includes:

- what you did, what you expected, and what actually happened,
- the affected component and version (server, client library and version, browser, or app),
- and, where possible, a minimal example or a small network that reproduces the problem.

Filing an issue first gives maintainers and the community a chance to discuss the change, and it gives your later pull request something concrete to reference. For anything touching the REST API or the CX data format, discussing the change up front is especially important, because those contracts are shared across many clients and services.

## Making Changes via Pull Request

The general workflow is the same across projects:

1. **Fork** the repository and create a branch for your change.
2. **Target the correct base branch.** NDEx projects follow semantic versioning: new features generally target the development/unstable branch, while bugfixes target the stable/release branch. Branch names vary by project — for example, `ndex3` uses `development` as its main integration branch — so check the project's README or its existing branches before opening your PR.
3. **Make your change,** keeping commits focused and readable.
4. **Include tests and documentation updates** where applicable (see below).
5. **Open a pull request** referencing the related issue, and respond to review feedback.

Keep pull requests focused on a single concern. If a change spans multiple repositories (for example, a REST server change and the client update that consumes it), open a PR in each and cross-link them so reviewers can see the whole picture.

Update documentation as part of your change rather than editing generated output directly. Each project documents where its source docs live; for API changes, update the OpenAPI specification rather than hand-editing generated API pages.

## Code Style

Favor readability and clarity over strict adherence to rules. Match the style of the surrounding code, and use each project's configured linter/formatter to keep formatting consistent:

- **JavaScript / TypeScript** projects (`ndex3`, `iquery`, `ndex-js-client`): use the configured ESLint setup (for example, `eslint --fix`) and follow the existing formatting.
- **Python** projects (`ndex2-client`): follow PEP 8 and the project's existing conventions.
- **Java** projects (`ndex-rest`, `ndex-object-model`, `ndex-java-client`, services): match the surrounding code and the project's build configuration.

The goal is code that is easy for others to read and understand.

## Testing

Bugfixes should come with a test that fails without the fix and passes with it. New features should come with tests that cover the new behavior. Run the project's test suite locally and make sure it passes before opening a pull request:

- **JavaScript / TypeScript**: run the project's unit tests (for example, `npm run test`) and, where the project provides them, end-to-end tests (for example, `npm run test:e2e`).
- **Python**: run the project's test suite (for example, via `pytest` or `tox`).
- **Java**: run the project's tests through its build (for example, `mvn test`).

UI and visualization changes may be better verified through a project's running app or demo pages than through unit tests alone — follow the project's guidance, and include screenshots in your pull request when a change is visual.
