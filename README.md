<p align="center">
  <img src="https://images.atomist.com/sdm/SDM-Logo-Dark.png">
</p>

# @atomist/sdm-pack-s3

[![atomist sdm goals](http://badge.atomist.com/T29E48P34/atomist/sdm-pack-s3/24939d09-fe00-4a7a-8d52-0fc4c9672100)](https://app.atomist.com/workspace/T29E48P34)
[![npm version](https://img.shields.io/npm/v/@atomist/sdm-pack-s3.svg)](https://www.npmjs.com/package/@atomist-seeds/sdm-pack)

An extension pack for an [Atomist][atomist]
software delivery machine (SDM). See the
[Atomist documentation][atomist-doc] for more information on the
concept of a software delivery machine and how to create and develop
an SDM.

Send your project's build output to S3 using this fabulous `publishToS3` goal.

[atomist-doc]: https://docs.atomist.com/ (Atomist Documentation)

## Using

In your software delivery machine project:

`npm install @atomist/sdm-pack-s3`

then in your `machine.ts`:

```typescript
import { publishToS3Goal } from "@atomist/sdm-pack-s3";

    const publish = publishToS3Goal({
        bucketName: "your-bucket-name",
        region: "us-west-2", // use your region
        filesToPublish: ["site/**/*.html", "more/files/to/publish"],
        pathTranslation: (filepath, inv) => filepath, // rearrange files if necessary
        pathToIndex: "site/index.html", // index file in your project
    });
```

If you need a build to happen before the publish, call `withProjectListener()` on that goal 
and pass a [GoalProjectListenerRegistration](https://docs.atomist.com/developer/goals-more/#prepare-the-checked-out-code).

Add this publish goal to one of your goal sets.

```typescript
    const publishGoals = goals("publish static site to S3")
        .plan(publish);

    sdm.withPushRules(
        whenPushSatisfies(requestsUploadToS3).setGoals(publishGoals),
    );
```

## Getting started

See the [Developer Quick Start][atomist-quick] to jump straight to
creating an SDM.

[atomist-quick]: https://docs.atomist.com/quick-start/ (Atomist - Developer Quick Start)

## Contributing

Contributions to this project from community members are encouraged
and appreciated. Please review the [Contributing
Guidelines](CONTRIBUTING.md) for more information. Also see the
[Development](#development) section in this document.

## Code of conduct

This project is governed by the [Code of
Conduct](CODE_OF_CONDUCT.md). You are expected to act in accordance
with this code by participating. Please report any unacceptable
behavior to code-of-conduct@atomist.com.

## Documentation

Please see [docs.atomist.com][atomist-doc] for
[developer][atomist-doc-sdm] documentation.

[atomist-doc-sdm]: https://docs.atomist.com/developer/sdm/ (Atomist Documentation - SDM Developer)

## Connect

Follow [@atomist][atomist-twitter] and [The Composition][atomist-blog]
blog related to SDM.

[atomist-twitter]: https://twitter.com/atomist (Atomist on Twitter)
[atomist-blog]: https://the-composition.com/ (The Composition - The Official Atomist Blog)

## Support

General support questions should be discussed in the `#support`
channel in the [Atomist community Slack workspace][slack].

If you find a problem, please create an [issue][].

[issue]: https://github.com/atomist-seeds/sdm-pack/issues

## Development

You will need to install [Node.js][node] to build and test this
project.

[node]: https://nodejs.org/ (Node.js)

### Build and test

Install dependencies.

```
$ npm install
```

Use the `build` package script to compile, test, lint, and build the
documentation.

```
$ npm run build
```

### Release

Releases are handled via the [Atomist SDM][atomist-sdm].  Just press
the 'Approve' button in the Atomist dashboard or Slack.

[atomist-sdm]: https://github.com/atomist/atomist-sdm (Atomist Software Delivery Machine)

---

Created by [Atomist][atomist].
Need Help?  [Join our Slack workspace][slack].

[atomist]: https://atomist.com/ (Atomist - How Teams Deliver Software)
[slack]: https://join.atomist.com/ (Atomist Community Slack)
