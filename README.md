# Rollcage
[![Circle CI](https://circleci.com/gh/circleci/rollcage.svg?style=svg)](https://circleci.com/gh/circleci/rollcage)
[![cljdoc](https://cljdoc.org/badge/circleci/rollcage)](https://cljdoc.org/d/circleci/rollcage/CURRENT)
[![Clojars Project](https://img.shields.io/clojars/v/circleci/rollcage.svg)](https://clojars.org/circleci/rollcage)


A Clojure client for [Rollbar](http://rollbar.com)


## Installation

Rollcage is available on [Clojars](https://clojars.org/circleci/rollcage).

### Leiningen/Boot

```clojure
[circleci/rollcage "1.0.203"]
```

### Clojure CLI/deps.edn

```clojure
circleci/rollcage {:mvn/version "1.0.203"}
```

## Quickstart

You can send exceptions like this:

```Clojure
user=> (require '[circleci.rollcage.core :as rollcage])

user=> (def r (rollcage/client "access-token" {:environment "staging"}))

user=> (try
  #_=>   (/ 0)
  #_=>   (catch Exception e
  #_=>     (rollcage/error r e)))
{:err 0, :result {:id nil, :uuid "420cfa6e-40d1-431d-80ef-575520c40dd7"}}
```

You can also setup handler for all UncaughtExceptions.
Call this fn during start-up procedure to ensure all uncaught exceptions
will be sent to Rollbar.

user=> (rollcage/setup-uncaught-exception-handler r)

See the full [API docs](https://cljdoc.org/d/circleci/rollcage/CURRENT) for more
information.

## Contributing

If you would like to contibute to the project, please [log an issue](https://cljdoc.org/d/circleci/rollcage/CURRENT) to discuss the feature/bug before submitting a pull request.

## Testing

A full CI suite is [run on CircleCI](https://circleci.com/gh/circleci/rollcage).
You can run the unit-test suite locally by running `lein test`. Some tests
require access to Rollbar, with a valid access token that has permission to post
server items. The token should be specified in the ROLLBAR_ACCESS_TOKEN
environment variable.

```bash
$ ROLLBAR_ACCESS_TOKEN=<your token> lein test
```

The tests that require access to Rollbar are annotated with the `:integration`
metadata tag. You can exclude these by using the `:unit` test selector.

```bash
$ lein test :unit
```


## Releasing

Releases are published [to Clojars under the CircleCI organisation](https://clojars.org/circleci/rollcage).
You can publish new SNAPSHOT version of Rollcage using leiningen:

```bash
$ lein deploy clojars
```

You can release a new version of Rollcage by editing the version string in
`project.clj` according to [semver](http://semver.org/) and removing the
`-SNAPSHOT` qualifier. Then run

```bash
$ lein deploy clojars
```

## License

Distributed under the [Eclipse Public License](http://www.eclipse.org/legal/epl-v10.html).
