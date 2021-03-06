## 0.8.2

* Bump `aeson` upper bound

* Fix `mtl` related deprecation warnings

## 0.8.1

* Export internal types

* Added `MonadBase`, `MonadTransControl` and `MonadBaseControl` instances for
  `ActionT`

## 0.8.0

* Upgrade to wai/wai-extra/warp 3.0

* No longer depend on conduit-extra.

* The `source` response method has been deprecated in favor
  of a new `stream` response, matching changes in WAI 3.0.

* Removed the deprecated `reqHeader` function.

## 0.7.3

* Bump upper bound for case-insensitive, mtl and transformers.

## 0.7.2

* Bump lower bound on conduit, add conduit-extra to cabal build depends.

## 0.7.1

* Default warp settings now use `setFdCacheDuration 0` to work around a warp
  issue where file changes are not getting picked up.

## 0.7.0

* Renamed `reqHeader` to `header`. Added `headers` function to get all headers.

* Changed `MonadIO` instance for `ActionT` such that IO exceptions are lifted
  into `ScottyError`s via `stringError`.

* Make `Bool` parsing case-insensitive. Goal: support both Haskell's True/False
  and Javascript's true/false. Thanks to Ben Gamari for suggesting this.

* Bump `aeson`/`text` upper bounds.

* Bump `wai`/`wai-extra`/`warp` bounds, including new lower bound for `warp`, which fixes a security issue related to Slowloris protection.

## 0.6.2

* Bump upper bound for `text`.

## 0.6.1

* Match changes in `wai-extra`.

## 0.6.0

* The Scotty transformers (`ScottyT` and `ActionT`) are now parameterized
  over a custom exception type, allowing one to extend Scotty's `ErrorT`
  layer with something richer than `Text` errors. See the `exceptions`
  example for use. `ScottyM` and `ActionM` remain specialized to `Text`
  exceptions for simplicity.

* Both monads are now instances of `Functor` and `Applicative`.

* There is a new `cookies` example.

* Internals brought up-to-date with WAI 2.0 and related packages.

## 0.5.0

* The Scotty monads (`ScottyM` and `ActionM`) are now monad transformers,
  allowing Scotty applications to be embedded in arbitrary `MonadIO`s.
  The old API continues to be exported from `Web.Scotty` where:

        type ScottyM = ScottyT IO
        type ActionM = ActionT IO

  The new transformers are found in `Web.Scotty.Trans`. See the
  `globalstate` example for use. Special thanks to Dan Frumin (co-dan)
  for much of the legwork here.

* Added support for HTTP PATCH method.

* Removed lambda action syntax. This will return when we have a better
  story for typesafe routes.

* `reqHeader :: Text -> ActionM Text` ==>
  `reqHeader :: Text -> ActionM (Maybe Text)`

* New `raw` method to set body to a raw `ByteString`

* Parse error thrown by `jsonData` now includes the body it couldn't parse.

* `header` split into `setHeader` and `addHeader`. The former replaces
  a response header (original behavior). The latter adds a header (useful
  for multiple `Set-Cookie`s, for instance).
