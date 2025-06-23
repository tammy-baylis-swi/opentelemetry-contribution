# From new user to community approver: how to grow as an OpenTelemetry contributor

## Abstract

What’s it like to start as a new end user then become an approver of the 2nd most active Cloud Native Computing Foundation (CNCF) project of all time, behind only Kubernetes? Learn the basics of OpenTelemetry (OTel) for Python, how to engage with a global community of developers, and how to start contributing to the open-source code base.

----

- [From new user to community approver: how to grow as an OpenTelemetry contributor](#from-new-user-to-community-approver-how-to-grow-as-an-opentelemetry-contributor)
  - [Abstract](#abstract)
  - [About this page](#about-this-page)
  - [Introduction to OpenTelemetry (OTel) in Python](#introduction-to-opentelemetry-otel-in-python)
    - [What is OTel?](#what-is-otel)
    - [What does OTel Python do?](#what-does-otel-python-do)
  - [How do I use OTel Python?](#how-do-i-use-otel-python)
    - [Manual instrumentation](#manual-instrumentation)
    - [Zero-Code instrumentation](#zero-code-instrumentation)
    - [Go beyond the posted examples](#go-beyond-the-posted-examples)
  - [How do I troubleshoot OTel Python?](#how-do-i-troubleshoot-otel-python)
  - [Let's contribute to OTel Python!](#lets-contribute-to-otel-python)
    - [Where is OTel Python?](#where-is-otel-python)
    - [What counts as a "contribution"?](#what-counts-as-a-contribution)
    - [Minimum requirements for all GitHub contributions](#minimum-requirements-for-all-github-contributions)
    - [It can help to participate in the OTel Python Community](#it-can-help-to-participate-in-the-otel-python-community)
    - [How to find a good first-time issue](#how-to-find-a-good-first-time-issue)
    - [What if I want to fix a new bug?](#what-if-i-want-to-fix-a-new-bug)
    - [What if I want to build a new feature?](#what-if-i-want-to-build-a-new-feature)
    - [Everyone appreciates fixes to the docs and examples too!](#everyone-appreciates-fixes-to-the-docs-and-examples-too)
    - [A note about implementing native support for OTel in your code](#a-note-about-implementing-native-support-for-otel-in-your-code)
    - [How to get your OTel Python PR reviewed](#how-to-get-your-otel-python-pr-reviewed)
    - [My PR got approved! What's next?](#my-pr-got-approved-whats-next)
  - [Why contribute to OTel Python?](#why-contribute-to-otel-python)
  - [How can I take my OTel Python contributions to the next level?](#how-can-i-take-my-otel-python-contributions-to-the-next-level)
    - [Become an official OTel Member](#become-an-official-otel-member)
    - [Become an OTel Python Approver](#become-an-otel-python-approver)
    - [What's after that?](#whats-after-that)
  - [Conclusion](#conclusion)

## About this page

This knowledge share is for my fellow Python developers, beginner to advanced, who are interested in making open-source code contributions to [OpenTelemetry (OTel)](https://opentelemetry.io/docs/): a codebase that defines and implements observability through the generation of traces, metrics, and logs. Readers will learn how to dive in and help progress nearly 100 of [OTel’s Python community packages](https://pypi.org/org/opentelemetry/) through end usage, code contribution, and further involvement.

The main focus of this content is contribution to OTel as an open-source project. While this gives a brief introduction to OTel Python and how it can be used, official example code already exists elsewhere and will be linked to as opposed to copied.


## Introduction to OpenTelemetry (OTel) in Python

Let's start with the basics of OTel Python as an open-source software project and what it provides for its end users.

### What is OTel?

[OTel](https://opentelemetry.io/docs/) is a vendor-neutral open source Observability framework. It's been a [Cloud Native Computing Foundation (CNCF) project](https://www.cncf.io/projects/opentelemetry/) since 2019. OTel is the [2nd most active CNCF project](https://www.cncf.io/blog/2024/11/15/gain-insights-into-cloud-native-applications-with-the-opentelemetry-certified-associate-otca/), topped only by Kubernetes.

OTel is supported by several languages, including Python -- the focus for this knowledge share. OTel for Python, or "OTel Python", is released by the community as [several, separate Python packages](https://pypi.org/org/opentelemetry/) that can be loosely divided into:

1. the core software developer kit (SDK)
2. instrumentation libraries (or "instrumentors")
3. exporters
4. distros

The functionality of the above components is defined by the [OTel Specification (spec)](https://opentelemetry.io/docs/specs/otel/) with most naming defined by the [OTel Semantic Conventions (semconv)](https://opentelemetry.io/docs/concepts/semantic-conventions/). But for an introduction to how OTel works, [Concepts](https://opentelemetry.io/docs/concepts/) will be an easier read. The Linux Foundation also offers a [free course, "Getting Started with OpenTelemetry"](https://training.linuxfoundation.org/blog/new-free-course-getting-started-with-opentelemetry-lfs148/), for those interested.

<img src="https://github.com/tammy-baylis-swi/opentelemetry-contribution/blob/4368ead6076157f0c031c49160810e18c7cd9201/img/what_is_otel.png">

### What does OTel Python do?

OTel Python's [SDK](https://opentelemetry.io/docs/languages/python/instrumentation/) implements the generation of telemetry to describe "what happened" to running code. [Traces](https://opentelemetry.io/docs/concepts/signals/traces/) consist of individual building blocks called spans, and they capture the path of a request through an application or multiple applications ([distributed tracing](https://opentelemetry.io/docs/concepts/context-propagation/)). [Metrics](https://opentelemetry.io/docs/concepts/signals/metrics/) are measurements of software availability and performance, such as call durations or CPU/memory usage by a process. [Logs](https://opentelemetry.io/docs/concepts/signals/logs/) are classic, timestamped text records that can be correlated with traces for more context and deeper debugging. See the linked documentation for more information on these three signals.

<img src="https://github.com/tammy-baylis-swi/opentelemetry-contribution/blob/4368ead6076157f0c031c49160810e18c7cd9201/img/signals.svg">

OTel Python's [instrumentation libraries](https://opentelemetry.io/docs/languages/python/libraries/) use the SDK to generate traces and metrics, either through [native support](https://opentelemetry.io/docs/languages/python/libraries/#use-natively-instrumented-libraries) (e.g. Elasticsearch client) or -- more commonly -- through community-managed instrumentors. The latter typically wrap common Python frameworks to intercept requests then describe them with trace and metrics generation. For example, [opentelemetry-instrumentation-flask](https://opentelemetry-python-contrib.readthedocs.io/en/latest/instrumentation/flask/flask.html) "instruments" a Flask server and generates telemetry over time as users make requests to the running service. See here for the [main list of community instrumentors](https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/instrumentation/README.md).

Using an OTel Python [distro](https://opentelemetry.io/docs/languages/python/distro/) provides users with a way to set up [zero-code instrumentation](https://opentelemetry.io/docs/zero-code/python/). If a distro installed, OTel is bootstrapped, and code of interest is run with the "instrument command" (more on this later), then there is no need to explicitly specify installation of every relevant instrumentation library nor initialize each of them in-code. Note that OTel Python manages an open-source, highly-configurable, ["default" distro](https://opentelemetry.io/docs/languages/python/distro/), while custom distros are offered by several vendors to work with their platforms.

[OTel Python's logs](https://opentelemetry.io/docs/languages/python/instrumentation/#logs) are not yet stable. But they can still be generated by directly setting up the [SDK's LoggingProvider and LoggingHandler](https://opentelemetry-python.readthedocs.io/en/stable/sdk/_logs.html). This forms a [logs bridge](https://opentelemetry.io/docs/specs/otel/logs/api/) that translates [Python standard logging](https://docs.python.org/3/library/logging.html) by apps to OTel log signals.

Finished telemetry signals from the SDK are exported to any destination configured by the user, such as to a running [OTel collector](https://opentelemetry.io/docs/collector/) (more on this later) or directly to a running backend. This requires an installed [OTel Python exporter](https://opentelemetry.io/docs/languages/python/exporters/). Two protocols are supported for transport: HTTP/Protobuf or gRPC. Once at the export destination, traces, metrics, and logs can be visually or programmatically analyzed to better understand "what happened" to instrumented code.


## How do I use OTel Python?

We use OTel Python by applying instrumentation to the Python code of our choice then seeing what telemetry signals are exported. This is also a great way to start to understand what it's doing under the hood, before starting to make contributions to the project. I recommend going through two different ways of setting this up: manual instrumentation and zero-code instrumentation (sometimes known as auto-instrumentation).

### Manual instrumentation

The core OTel Python repo provides three pared-down, simple examples one can copy or take inspiration from for the easiest way to set up manual instrumentation:

1. [OTel Python trace/span script](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples/basic_tracer)
2. [OTel Python metrics script](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples/metrics/instruments)
3. [OTel Python logs script](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples/logs)

All three examples consist of Python code that _manually_ calls the OTel Python SDK to generate individual telemetry signals.

The trace/span script uses the ConsoleSpanExporter to export spans to stdout. Meanwhile, the metrics and logs examples go a step further and set up OTLP exporters, plus a command to run the [OTel collector](https://opentelemetry.io/docs/collector/) I previously hinted at. Briefly, the OTel collector is an open-source, vendor-agnostic implementation that lets us receive, process, and export telemetry through any pipelines we configure. By default, OTel Python's OTLP exporters export to localhost endpoints that are typically occupied by the OTel collector for receiving. In the two examples for metrics and logs, the OTel collector is configured to export those signals to stdout via a "debug" exporter.

If manual instrumentation setup is complete and correct, then running your script(s) should show what traces/spans, metrics, and logs look like! This is through use of OTel Python's SDK and exporters alone.

### Zero-Code instrumentation

OTel Python can instrument all sorts of things: short-lived Python scripts, long-running web services using common frameworks (e.g. Flask, FastAPI), ORM-based (e.g. SQLAlchemy) or pure driver-based database clients, AWS Lambda functions, containerized apps in Kubernetes, GenAI-integrated apps, and more. However, adding and upkeeping manual OTel Python SDK calls throughout more complex code is often too much work! Therefore, OTel Python also includes instrumentation libraries for common frameworks and a default distro to not only reduce the overhead of added code, but also manage the installation of the additional libraries used to generate common spans and metrics for us.

The [starter docs](https://opentelemetry.io/docs/zero-code/python/) for installing and using OTel Python's default distro show how to instrument any `myapp.py` with basic configuration, and without any additional code. The [example doc](https://opentelemetry.io/docs/zero-code/python/example/) and OTel Python repo's [example code](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples/auto-instrumentation) demonstrate how to auto-instrument a Flask server so that any received HTTP requests result in trace/span and metrics generation. Try setting up a Flask app with an [OTel collector](https://opentelemetry.io/docs/collector/) configured to export telemetry to debug/console.

If zero-code instrumentation setup is complete and correct, then running your server app and making HTTP requests to it should show what traces/spans, metrics, and any logs look like. This is through use of OTel Python's framework-wrapping instrumentation libraries, the SDK, and exporters.


### Go beyond the posted examples

Once you're comfortable with manual and/or zero-code instrumentation, you could try more complex use cases to see how far the current state of OTel Python can take you. Some examples:

1. Configure [OTel collector](https://opentelemetry.io/docs/collector/) to export to a backend with cool features and GUIs. Free platforms include Prometheus and Jaeger, else free trials are available for platforms like [SolarWinds Observability](https://www.solarwinds.com/solarwinds-observability).
2. Instrument several HTTP servers that make requests to one another to generate [distributed traces](https://opentelemetry.io/docs/concepts/context-propagation/).
3. Opt into [sqlcommenter](https://opentelemetry-python-contrib.readthedocs.io/en/latest/instrumentation/mysql/mysql.html#sqlcommenter) for a database client application and check the server general logs for potential db context propagation.
4. Apply OTel's [Python auto-instrumentation layer](https://opentelemetry.io/docs/platforms/faas/lambda-auto-instrument/) to an AWS Lambda function.
5. Use OTel's [Kubernetes Operator](https://opentelemetry.io/docs/platforms/kubernetes/) with the [Python auto-instrumentation image](https://opentelemetry.io/docs/platforms/kubernetes/operator/automatic/).


## How do I troubleshoot OTel Python?

If I have a general question about OTel Python, then I'll do one of these things:
1. Search the [OTel.io docs](https://opentelemetry.io). There are dedicated "Troubleshooting" pages for some topics, such as this one for OTel Python zero-code instrumentation:
   * https://opentelemetry.io/docs/zero-code/python/troubleshooting/
2. Browse the OTel Python-specific docs that are published to ReadTheDocs:
   * https://opentelemetry-python.readthedocs.io/en/latest/index.html
   * https://opentelemetry-python-contrib.readthedocs.io/en/latest/index.html

If I have a specific issue while trying to use OTel Python, I generally follow these steps:
1. Read any tracebacks or warning logs! The source code is here under two repos for "core" and "contrib":
   * https://github.com/open-telemetry/opentelemetry-python/
   * https://github.com/open-telemetry/opentelemetry-python-contrib/
2. If stuck, post any ad hoc question to `#otel-python` channel in [CNCF's Slack Workspace](https://communityinviter.com/apps/cloud-native/cncf).
   * [Keep comms respectful](https://github.com/open-telemetry/community/blob/main/code-of-conduct.md) and don't be shy!
   * Be prepared to share steps and/or code to reproduce the issue.
3. Check to see if others might be experiencing the same issue:
   * https://github.com/open-telemetry/opentelemetry-python/issues
   * https://github.com/open-telemetry/opentelemetry-python-contrib/issues

If I haven't found a solution after trying all of the above, then maybe it's time to contribute to OTel Python!


## Let's contribute to OTel Python!

### Where is OTel Python?

Most of OTel is public under the [GitHub organization "open-telemetry"](https://github.com/open-telemetry/), including the OTel Python repos I've already mentioned for [core](https://github.com/open-telemetry/opentelemetry-python/) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/). GitHub provides the community's contributors with version control and CI/CD of not just the code but also the [spec](https://github.com/open-telemetry/opentelemetry-specification/), [semconv](https://github.com/open-telemetry/semantic-conventions/), [docs](https://github.com/open-telemetry/opentelemetry.io/), and more components shared across languages. GitHub is also where issues are posted to track work and discussion, while project boards are managed for larger efforts.

### What counts as a "contribution"?

Given the above, a "contribution" to OTel is [anything that counts as a contribution to GitHub](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/viewing-contributions-on-your-profile#what-counts-as-a-contribution):

* Committing to a repository's default branch or gh-pages branch
* Creating a branch
* Opening an issue
* Opening a discussion
* Answering a discussion
* Proposing a pull request (PR)
* Submitting a pull request review

If you'd like to enhance OTel Python because you noticed something that could be improved, or you know the fix to a problem that others are facing, then any of the above are part of reporting bugs/features and working on PRs for OTel Python! The rest of this section focuses on how to do this.

### Minimum requirements for all GitHub contributions

The main requirement, common to all OTel repos and before you start working on your first OTel PR, is to associate your public GitHub account with [CNCF's Contributor License Agreement (CLA)](https://github.com/open-telemetry/community/blob/main/guides/contributor/CLA.md) using [Linux Foundation's EasyCLA](https://easycla.lfx.linuxfoundation.org/#/?version=2). This is a one-time process and will link your work either as an individual contributor or a corporate contributor (i.e. through your work email). This is required for all checks to pass on your OTel PRs:

<img src="https://github.com/tammy-baylis-swi/opentelemetry-contribution/blob/4368ead6076157f0c031c49160810e18c7cd9201/img/easycla.png">

Make sure to also review OTel's [community guidelines](https://github.com/open-telemetry/community/blob/main/code-of-conduct.md) to maintain a welcoming, collaborative environment.

### It can help to participate in the OTel Python Community

I previously mentioned the `#otel-python` channel in [CNCF's Slack Workspace](https://communityinviter.com/apps/cloud-native/cncf) as a place to ask questions about OTel Python end usage. It is not required that you join, but Slack can also be a helpful place to bring up and discuss any GitHub issues, PRs, or early ideas for them.

For the most synchronous way to talk about anything OTel Python, feel free to join the Python Special Interest Group (SIG) meeting on Zoom. It is held every Thursday 09:00AM PDT/PST (UTC-7h/UTC-8h) with room link listed in the [OpenTelemetry Google Calendar](https://calendar.google.com/calendar/embed?src=c_2bf73e3b6b530da4babd444e72b76a6ad893a5c3f43cf40467abc7a9a897f977%40group.calendar.google.com). Newcomers are always welcome to say Hi and ask questions.


### How to find a good first-time issue

If you'd like to contribute to OTel Python but aren't sure about what changes to make, there are already posted issues and many of them labelled "good first issue"! See these [core](https://github.com/open-telemetry/opentelemetry-python/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22) issue queries.

In my personal opinion, it might be easier to start with a [contrib issue](https://github.com/open-telemetry/opentelemetry-python-contrib/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22). Currently, it is the framework-specific instrumentation libraries that have the most room for improvement that is already spec'd out. For example, several instrumentors need to be updated to assign [attributes following the latest semconv](https://github.com/open-telemetry/opentelemetry-python-contrib/issues/1624). Some of them need to start [generating metrics](https://github.com/open-telemetry/opentelemetry-python-contrib/issues/1040) and this is typically an additive change. Conversely, the core repo is mostly stable and any fixes/enhancements typically require debugging complex, historical code. That being said, [OTel Python's Logging API](https://github.com/orgs/open-telemetry/projects/123) is in urgent need of stabilization.


### What if I want to fix a new bug?

What if OTel Python is not behaving as expected? You may have already checked the existing [core](https://github.com/open-telemetry/opentelemetry-python/issues?q=is%3Aissue%20state%3Aopen%20label%3Abug) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/issues?q=is%3Aissue%20state%3Aopen%20label%3ABug) bug-labelled issues and nobody else has reported what you've seen. You may have also done a search in `#otel-python` channel in [CNCF's Slack Workspace](https://communityinviter.com/apps/cloud-native/cncf) but nothing came up. Then, the next step is to create a new bug issue!

First, try to figure out which OTel Python repo should house the new issue. If your instrumentation setup produced a traceback or any logs, then you can try to narrow down which part of the codebase might be problematic. If it's still not clear, that's ok! Issues can always be edited and moved later.

Next, click "New Issue" for either [core](https://github.com/open-telemetry/opentelemetry-python/issues) or [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/issues) repo. Follow the prompt for "Bug Report" then fill out all fields before submitting. On the newly-created issue, comment that you'd like to contribute a fix.

To make code changes, start by forking a copy of the [core](https://github.com/open-telemetry/opentelemetry-python) or [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib) repo into your own account, i.e. the same account under which you signed with EasyCLA. From your fork, check out a new branch. This will be the branch you eventually use to merge into the original repo's `main` branch.

Both [core](https://github.com/open-telemetry/opentelemetry-python/blob/main/CONTRIBUTING.md) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/CONTRIBUTING.md) repos have helpful `CONTRIBUTING.md` that outline how to set up your local environment for development. Remember to lint and run unit tests regularly. See below for how to start getting your PR reviewed.


### What if I want to build a new feature?

Preparing to build a new OTel Python feature is very similar to fixing a bug. The main differences are:

1. [Check the specs!](https://opentelemetry.io/docs/specs/)
2. Report a "Feature Request" instead of a "Bug Report" issue.

Previously, I mentioned that the core repo is mostly stable (except for some components such as [OTel Python's Logging API](https://github.com/orgs/open-telemetry/projects/123)). The contrib repo's instrumentors are also stable in some ways such as the number of spans that should be generated by each framework's traced call -- fundamental behaviours like this should not be changed. But support for new functionality can sometimes be added as an opt-in feature or even a breaking feature, depending on what exactly it would do.

If there is a feature that you'd like to build, feel free to create an issue and a draft PR to help illustrate what it would do. Also keep in mind that the feature should not directly contradict what the OTel [spec](https://opentelemetry.io/docs/specs/otel/) and [semconv](https://opentelemetry.io/docs/concepts/semantic-conventions/) describe. Note that these documents are kept intentionally vague in some parts to accommodate the particulars of each language in which OTel is implemented, not just Python. See below for how to start getting your PR reviewed.


### Everyone appreciates fixes to the docs and examples too!

GitHub contributions to OTel definitely still count for changes that aren't necessarily bugfixes nor features. While learning OTel for the first time or while diving deep into the code, you will probably encounter a mistake or outdated part of some markdown, docstring, comment, code snippet, or something else.

For something small like a typo fix, simply put in a [core](https://github.com/open-telemetry/opentelemetry-python) or [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib) PR and the Maintainers can skip the Changelog check for you. No need to create a new GitHub issue.

For something bigger like a new [example](https://github.com/open-telemetry/opentelemetry-python/tree/main/docs/examples), submit a new "Feature Request" issue to accompany your PR.

Feel welcome to also put in PRs to update the [otel.io docs](https://opentelemetry.io/docs/), whose [source code is here](https://github.com/open-telemetry/opentelemetry.io/).

See below for how to start getting your PR reviewed.


### A note about implementing native support for OTel in your code

I briefly mentioned [native support](https://opentelemetry.io/docs/languages/python/libraries/#use-natively-instrumented-libraries) of OTel by some Python libraries that aren't necessarily [community-managed instrumentors](https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/instrumentation/README.md). Building such a library would involve implementing one's own collection of telemetry signals, which any developer is welcome to do! Just note that you may not necessarily need to change any of the code in OTel Python's [core](https://github.com/open-telemetry/opentelemetry-python/) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/). Instead, I suggest doing these:

1. As with a new community feature, make sure the native instrumentation still aligns with OTel [spec](https://opentelemetry.io/docs/specs/otel/) and [semconv](https://opentelemetry.io/docs/concepts/semantic-conventions/).
2. Consider asking for end user and OTel Python Maintainer feedback early in design/development in [CNCF's Slack](https://communityinviter.com/apps/cloud-native/cncf) and the [Python SIG meetings](https://calendar.google.com/calendar/embed?src=c_2bf73e3b6b530da4babd444e72b76a6ad893a5c3f43cf40467abc7a9a897f977%40group.calendar.google.com).
3. Once released, [submit a new issue to update the docs](https://opentelemetry.io/docs/languages/python/libraries/#use-natively-instrumented-libraries) so that they can showcase your library!


### How to get your OTel Python PR reviewed

When your OTel Python changes are ready for review, create a PR from your fork's fix/feature branch into the original repo's `main` branch. I recommend creating a draft PR first in order to get the PR number and iron out any CI/CD failures before GitHub automatically notifies pre-configured reviewers. Immediately after creating the PR, add and commit a descriptive, concise line with the PR's url under "Unreleased" in `CHANGELOG.md` ([core](https://github.com/open-telemetry/opentelemetry-python/blob/main/CHANGELOG.md?plain=1) or [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/CHANGELOG.md?plain=1)).

At the bottom of your PR, there may be a report of CI/CD passes and failures related to formatting, unit tests, and more. If you don't have permission to run these, that's ok as an Approver or Maintainer can run them later. Whether or not the CI/CD has run, make sure linting and unit tests pass on your local. See [core](https://github.com/open-telemetry/opentelemetry-python/blob/main/CONTRIBUTING.md) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/CONTRIBUTING.md) `CONTRIBUTING.md` files for how to do this.

Then, mark the PR as "Ready". This will automatically ping members of [python-approvers](https://github.com/orgs/open-telemetry/teams/python-approvers) or [opentelemetry-python-contrib-approvers](https://github.com/orgs/open-telemetry/teams/opentelemetry-python-contrib-approvers) with requests for review. Feel free to also add individual reviewers you've been collaborating with. If your PR is for the [otel.io docs source code](https://github.com/open-telemetry/opentelemetry.io/), the [docs-approvers](https://github.com/orgs/open-telemetry/teams/docs-approvers) will be assigned instead.

If it has been several days and nobody has reviewed your PR, most likely it's because the OTel Python Approvers and Maintainers don't currently have enough bandwidth to do so -- most of them are part-time contributors too! Keeping this in mind, you may post in `#otel-python` channel in [CNCF's Slack Workspace](https://communityinviter.com/apps/cloud-native/cncf) to ask for others to have a look. You can also attend the Python SIG meetings mentioned above (see [OpenTelemetry Google Calendar](https://calendar.google.com/calendar/embed?src=c_2bf73e3b6b530da4babd444e72b76a6ad893a5c3f43cf40467abc7a9a897f977%40group.calendar.google.com) for Zoom link) to ask for feedback.

As Approvers and Maintainers leave feedback, address them with additional commits and/or comments and re-request reviews as needed.


### My PR got approved! What's next?

Getting an OTel PR approved takes effort -- congratulations!

For OTel Python, changes can only be merged by [python-maintainers](https://github.com/orgs/open-telemetry/teams/python-maintainers) or [opentelemetry-python-contrib-maintainers](https://github.com/orgs/open-telemetry/teams/opentelemetry-python-contrib-maintainers). These Maintainers merge PRs in a specific order and to time correctly with the publishes that they also manage. It is worth noting that both OTel Python mono-repos currently house the source code of [multiple packages](https://pypi.org/org/opentelemetry/) that are released in lockstep (see also releases for [core](https://github.com/open-telemetry/opentelemetry-python/releases) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/releases)). Therefore, the changes made through your PR will most likely be part of several changes made by a collective of contributors and part of the next OTel Python release. The release cadence is typically once per month for minor version releases.


## Why contribute to OTel Python?

Here are the benefits we get from contributing to OTel Python:

1. We make OTel Python better and easier for future users through code and documentation improvements.
2. We fix the bugs we want fixed, and implement the additional features we want.
   * Or, we bring attention to bugs/features and other contributors might work on them.
3. We more quickly learn OTel as a an observability framework than end usage alone, while we learn to navigate a complex, open-source project.
4. We receive guidance from experienced and well-intentioned people in the community.
5. We gain exposure as individuals and (if applicable) for our organizations.
   * With enough contributions, your username will appear on [this DevStats table](https://opentelemetry.devstats.cncf.io/d/22/prs-authors-table?orgId=1).
   * If your account is associated with your employer, your company could rank on [this DevStats table](https://opentelemetry.devstats.cncf.io/d/5/companies-table).
   * After a lot of contributions to a particular repo, you may appear in a Thank You section!:

<img src="https://github.com/tammy-baylis-swi/opentelemetry-contribution/blob/4368ead6076157f0c031c49160810e18c7cd9201/img/thank_you_repo.png">

There are also some challenges to consider:

1. Changes are not super quick because of a lack of contributors.
2. The OTel [semconv](https://github.com/open-telemetry/semantic-conventions/) is dense and vast because it's been built over several years. It can be challenging to read and navigate.​
3. The OTel [specs](https://github.com/open-telemetry/opentelemetry-specification/) are intentionally a little vague to accommodate different languages, so not everything is 1:1 across languages.​
4. Stable features can be enhanced with opt-in additions, but can't be fundamentally changed, e.g.:​ numbers of spans and how Python's implementation of spans is mostly immutable. So some but not all new features will be accepted.


## How can I take my OTel Python contributions to the next level?

The biggest issue OTel faces is a lack of contributors. There is always lots to do! Whether you are a new or long-term OTel Python user, or just getting back into things, you are welcome to keep contributing issues and PRs. This section describes what else contributors can do to participate in OTel more regularly.

The community's [Membership, Roles, and Responsibilites guide](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md) lists all current information and detailed requirements. On this page, I will focus on my personal experiences as someone accepted as an Approver.

### Become an official OTel Member

After completing a few issues and PRs, OTel Python contributors are welcome to apply to become official [OTel Members](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#member). The main requirement for this is to [open a Community repo issue](https://github.com/open-telemetry/community/issues/new?template=membership.md&title=REQUEST%3A%20New%20membership%20for%20%3Cyour-GH-handle%3E) with sponsorship from two members of either [python-approvers](https://github.com/orgs/open-telemetry/teams/python-approvers) or [opentelemetry-python-contrib-approvers](https://github.com/orgs/open-telemetry/teams/opentelemetry-python-contrib-approvers). If you're not already in direct contact with Approvers, then you can ask for sponsors in the `#otel-python` channel in [CNCF's Slack Workspace](https://communityinviter.com/apps/cloud-native/cncf) or at the Python SIG meeting (see [OpenTelemetry Google Calendar](https://calendar.google.com/calendar/embed?src=c_2bf73e3b6b530da4babd444e72b76a6ad893a5c3f43cf40467abc7a9a897f977%40group.calendar.google.com) for Zoom link). The main benefits of membership are being eligible to vote for OTel's [Governance Committee (GC)](https://github.com/open-telemetry/community/blob/main/governance-charter.md), and increased reputation during participation in issues and PRs. Members are also encouraged to review the PRs of other contributors.


### Become an OTel Python Approver

Once you've reviewed several PRs and created more of your own, consider applying to become an [Approver](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#approver) for OTel Python! This is the official title I currently hold in the OTel community. The role can be challenging and time-consuming, but rewarding.

I've mentioned several times now that [CNCF's Slack](https://communityinviter.com/apps/cloud-native/cncf) and the [Python SIG meetings](https://calendar.google.com/calendar/embed?src=c_2bf73e3b6b530da4babd444e72b76a6ad893a5c3f43cf40467abc7a9a897f977%40group.calendar.google.com) are helpful for troubleshooting OTel end usage, feature ideas, and PR reviews. Once you are an OTel Python Approver, checking Slack and attending the meetings should now be part of your regular duties if your time zone permits it. It also helps to provide some insight for the questions that other community members post.

OTel Python Approvers often help with issue triage. This does not require Approver status generally speaking, but OTel Python does not maintain a separate "Triagers" group. Newly-submitted issues might be missing labels (e.g. bug verses feature, "good first issue"), or may not have enough information about the problem experienced. In the latter case, we leave a comment on the issue requesting more info.

To go with the namesake, OTel Python Approvers regularly review PRs in [core](https://github.com/open-telemetry/opentelemetry-python/) and [contrib](https://github.com/open-telemetry/opentelemetry-python-contrib/). I often take this approach to OTel Python PRs, which is based on the community's [Responsibilities and Privileges](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#responsibilities-and-privileges-2):

1. What is the impact that the changes will make?
   * The PR original description should link to a descriptive GitHub issue before the PR can be approved.
   * Is there an existing workaround?
2. Do the changes align with the OTel [spec](https://github.com/open-telemetry/opentelemetry-specification/) and/or [semconv](https://github.com/open-telemetry/semantic-conventions/)?
   * Will the changes simply implement what's already defined?
   * Should the spec or semcov be updated first, before Python code changes?
   * Will the changes contradict stable requirements?
3. Will the PR changes be cohesive with the existing code, with minimizal code complexity and less friction for end users? See also the community's [Engineering Values](https://opentelemetry.io/community/mission/#engineering-values).
4. Then: does the Python code make sense and do all checks pass?

Approvers have permission to trigger CI/CD runs on PRs as required. If you're ever unsure, you can message other Approvers on Slack or ask at the Python SIG meeting. Note that, at this time, it is the OTel Python Maintainers that can actually merge PR code.

As a long-term contributor and OTel Python Approver, occasionally I contribute to other OTel repos and participate in other communications/SIGs. I've previously mentioned the [otel.io docs repo](https://github.com/open-telemetry/opentelemetry.io/), where I've submitted PRs and reviewed other PRs. I have also worked on issues and PRs for [opentelemetry-operator](https://github.com/open-telemetry/opentelemetry-operator/) and [opentelemetry-lambda](https://github.com/open-telemetry/opentelemetry-lambda/), which each build using OTel Python.

With all communications within the OTel, especially when increased as an official Member or Approver, always remember that the [Community Values](https://opentelemetry.io/community/mission/#community-values) apply to everyone. Keep in mind that OTel is a project worked on by people from different cultural backgrounds. Messaging should be clear, with some politeness, and without rudeness and attacks. The [Code of Conduct](https://github.com/open-telemetry/community/blob/main/code-of-conduct.md) outlines how to address inapproprate behaviour. SIGs like OTel Python have a [dedicated GC liaison](https://github.com/open-telemetry/community/blob/main/sigs.yml) for a direct point of contact on Slack if needed.

The Approver role is a great position to give and receive mentorship. Comments on PRs and issues are opportunities to share knowledge and guide others, e.g. to "where everything is" for OTel. The community collectively consists a wide range of developer skills and experiences. While several OTel contributors are part of a larger "vendor-sphere" and may implement features to help with private software products, such changes must be generic and the community favours collaboration over competition. 


### What's after that?

All OTel contributors are encouraged to attend [CNCF events](https://www.cncf.io/events/). I recommend KubeCon + CloudNativeCon, and the Open Observability Summits + OTel Community Days that are hosted globally. These are a fun, synchronous way to meet other contributors, learn about the current goals of the GC ad TC, and see what others have built or investigated using OTel and other CNCF projects.

If interested, consider participating in the active projects of [other SIGs](https://github.com/open-telemetry/community/tree/main?tab=readme-ov-file#specification-sigs) to increase breadth of knowledge in the OTel domain. For example, in 2025 there is lots to do for Specification of OTel Configuration across languages and instrumentation of GenAI.

The next level of progression up the OTel ladder after Approver is to become a [Maintainer](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#maintainer). For OTel Python, Maintainers have the authority to merge PRs and facilitate the monthly releases of the [OTel’s Python packages](https://pypi.org/org/opentelemetry/). They must also communicate regularly with the Approvers and other Maintainers, run the SIG meetings, and represent OTel Python when discussing topics with other SIGs, OTel's [Technical Committee (TC)](https://github.com/open-telemetry/community/blob/2f2c7c1bc051dbe0483fb3795965ee3c83f826f4/tech-committee-charter.md), and the [GC](https://github.com/open-telemetry/community/blob/main/governance-charter.md). It is a highly involved role.

After being a super contributor for some years, one might want to help steer top-level decisions made in the OTel community. If that's the case, consider nomination for the [TC and GC](https://github.com/open-telemetry/community/tree/main?tab=readme-ov-file#governing-bodies), OTel's governing bodies.


## Conclusion

In my opinion, it is worth it in the long-term to be both an OTel end user and a regular contributor.

1. OTel is popular for a reason. OTel Python provides highly-configurable observablity libraries for generation and inspection of traces, metrics, and logs to know what my software is doing.
2. Resources for troubleshooting OTel Python are a little scattered but do exist, including a welcoming environment of other developers on Slack and Zoom.
3. OTel Python contributions of any size are worthwhile and appreciated: bugfixes, features, and docs.
4. Becoming an OTel Member then OTel Python Approver has been valuable for advancing OTel while mentoring and learning from others.
5. There is always lots to do in the OTel community and we'd love more contributors!
