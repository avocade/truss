<a href="https://www.taoensso.com/clojure" title="More stuff by @ptaoussanis at www.taoensso.com"><img src="https://www.taoensso.com/open-source.png" alt="Taoensso open source" width="340"/></a>  
[**Documentation**](#documentation) | [Latest releases](#latest-releases) | [Get support][GitHub issues]

# Truss

#### Assertions micro-library for Clojure/Script

**Truss** is a tiny Clojure/Script library that provides fast and flexible **runtime assertions** with **terrific error messages**. Use it as a complement or alternative to [clojure.spec](https://clojure.org/about/spec), [core.typed](https://github.com/clojure/core.typed), etc.

<img src="hero.png" width="600" alt="Egyptian ship with rope truss, the oldest known use of trusses (about 1250 BC)."/>

> A doubtful friend is worse than a certain enemy. Let a man be one thing or the other, and we then know how to meet him. - Aesop

## Latest release/s

- `2023-07-15` `1.10.1`: [changes](../../releases/tag/v1.10.1)

[![Main tests][Main tests SVG]][Main tests URL]
[![Graal tests][Graal tests SVG]][Graal tests URL]

See [here][GitHub releases] for earlier releases.

## Why Truss?

- **Tiny** cross-platform Clj/s codebase with **zero dependencies**
- **Trivially easy** to learn, use, and understand
- **Terrific error messages** for quick+easy debugging
- **Terrific performance**: miniscule (!) runtime cost
- Easy **elision** for *zero* runtime cost
- No commitment or costly buy-in: use it just when+where needed
- Perfect for library authors: no bulky dependencies

## Quickstart

1\. Add the [relevant dependency](#latest-releases) to your project:

```clojure
Leiningen: [com.taoensso/truss               "x-y-z"] ; or
deps.edn:   com.taoensso/truss {:mvn/version "x-y-z"}
```

2\. Setup your namespace imports:

```clojure
(ns my-ns (:require [taoensso.truss :as truss :refer (have have! have?)]))
```

3\. Truss uses the simple `(predicate arg)` pattern familiar to Clojure users:

```clojure
(defn square [n]
  (let [n (have integer? n)] ; <- A Truss assertion
    (* n n)))

;; This assertion basically expands to:
;; (if (integer? n) n (throw-detailed-assertion-error!))

(square 5)   ; => 25
(square nil) ; =>
;; Invariant failed at truss-examples[9,11]: (integer? n)
;; {:dt #inst "2023-07-31T09:56:10.295-00:00",
;;  :pred clojure.core/integer?,
;;  :arg {:form n, :value nil, :type nil},
;;  :env {:elidable? true, :*assert* true},
;;  :loc
;;  {:ns truss-examples,
;;   :line 9,
;;   :column 11,
;;   :file "examples/truss_examples.cljc"}}
```

That's everything most users will need to know, but see the [documentation](#documentation) for more.

## Documentation

- [Full documentation][GitHub wiki] (detailed usage, etc.)
- Auto-generated API reference: [Codox][Codox docs], [clj-doc][clj-doc docs]

## Motivation

<a href="https://youtu.be/gMB4Y-EIArA" title="Truss talk (YouTube)">
<img src="https://raw.githubusercontent.com/ptaoussanis/truss/master/talk.jpg" width="600"/>
</a>

See [here][GitHub wiki] for more.

## Funding

You can [help support continued work][funding] on this project, thank you!! 🙏

Copyright &copy; 2015-2023 [Peter Taoussanis][].  
Licensed under [EPL 1.0](LICENSE.txt) (same as Clojure).

## License

Copyright &copy; 2014-2023 [Peter Taoussanis][].  
Licensed under [EPL 1.0](LICENSE.txt) (same as Clojure).

<!-- Common -->

[GitHub releases]: ../../releases
[GitHub issues]:   ../../issues
[GitHub wiki]:     ../../wiki

[Peter Taoussanis]: https://www.taoensso.com
[funding]:          https://www.taoensso.com/clojure/backers

<!-- Project -->

[Codox docs]:   https://taoensso.github.io/truss/
[clj-doc docs]: https://cljdoc.org/d/com.taoensso/truss/

[Clojars SVG]: https://img.shields.io/clojars/v/com.taoensso/truss.svg
[Clojars URL]: https://clojars.org/com.taoensso/truss

[Main tests SVG]:  https://github.com/taoensso/truss/actions/workflows/main-tests.yml/badge.svg
[Main tests URL]:  https://github.com/taoensso/truss/actions/workflows/main-tests.yml
[Graal tests SVG]: https://github.com/taoensso/truss/actions/workflows/graal-tests.yml/badge.svg
[Graal tests URL]: https://github.com/taoensso/truss/actions/workflows/graal-tests.yml
