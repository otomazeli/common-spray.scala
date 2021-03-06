# Change Log

## 0.24.0 ([#47](https://git.mobcastdev.com/Platform/common-spray/pull/47) 2015-01-02 11:30:51)

Default rejection handler

### New Feature

- `RejectionHandler` that converts Spray rejections into responses with JSON error messages

## 0.23.0 ([#46](https://git.mobcastdev.com/Platform/common-spray/pull/46) 2014-12-01 10:57:11)

v2 API Image representation

### New feature

- v2 API `Image` case class.

## 0.22.2 ([#45](https://git.mobcastdev.com/Platform/common-spray/pull/45) 2014-11-27 11:54:11)

Fixed a bug and updated metrics library

### Bug fixes

- The error body for `RejectedExecutionException` being thrown is now
correctly reported as service unavailable rather than internal server
error.

### Improvements

- Updated the version of the metrics library, and a couple of other
shared libraries.

## 0.22.1 ([#44](https://git.mobcastdev.com/Platform/common-spray/pull/44) 2014-11-26 18:02:35)

Bumped versions

### Improvements

- Bumped versions

## 0.22.0 ([#43](https://git.mobcastdev.com/Platform/common-spray/pull/43) 2014-11-26 17:36:02)

Returns right status for full thread pools

### New features

- Now returns `503 Service Unavailable` if the service code throws a
`RejectedExecutionException`, which occurs if an item cannot be added
to a bounded thread pool.

## 0.21.0 ([#42](https://git.mobcastdev.com/Platform/common-spray/pull/42) 2014-11-24 14:44:18)

Changed logging to use scala-logging (again...)

### Breaking Changes

- Logging now uses the Typesafe scala-logging library rather than the
SLF4J loggers. This _should_ work correctly this time…
- Now only supports Scala 2.11 as the logging library does not work
with 2.10

### Notes

- The json4s version is now 3.2.11 which adds a new method in
`DefaultFormats`; if you have references to older versions then this
can result in `AbstractMethodException` so make sure all your versions
are consistent. `common-json` has already been updated.

## 0.20.0 ([#41](https://git.mobcastdev.com/Platform/common-spray/pull/41) 2014-11-19 11:49:08)

Json error responses

### Breaking Change

- Added support for v2 API error messages in exception handler used by monitor directive. For example, `500 Internal Server Error` responses now contain JSON body:
```json
{"code":"InternalServerError","developerMessage":"There was an internal server error."}
```

## 0.19.1 ([#39](https://git.mobcastdev.com/Platform/common-spray/pull/39) 2014-11-13 17:27:25)

Monitoring directive logger fix

### Bugfix

Typesafe Logging library has a bizarre bug that results in attempts to log with a default implementation of `com.typesafe.scalalogging.Logger` that has no implementation when the logger is passed as a parameter to other methods.  :see_no_evil:

## 0.19.0 ([#37](https://git.mobcastdev.com/Platform/common-spray/pull/37) 2014-11-13 12:02:12)

V2 links

### New feature

- Added `Link` class

## 0.18.0 ([#36](https://git.mobcastdev.com/Platform/common-spray/pull/36) 2014-11-10 15:42:02)

Monitoring directive now uses typesafe Logger

### Breaking changes

- The `monitor` directive now expects a
`com.typesafe.scalalogging.Logger` rather than an `org.slf4j.Logger`
instance.

## 0.17.5 ([#35](https://git.mobcastdev.com/Platform/common-spray/pull/35) 2014-11-04 15:31:12)

Use strict mode option parsing by default

patch

- Use strict mode for parsing by default. 

## 0.17.4 ([#34](https://git.mobcastdev.com/Platform/common-spray/pull/34) 2014-11-04 09:30:30)

Support Validation of Optional fields

patch 

- Optionally throw a MappingException when a value for a key of type `Option[T]` can't be converted to a `T` when parsing json. 

## 0.17.3 ([#33](https://git.mobcastdev.com/Platform/common-spray/pull/33) 2014-10-15 15:10:14)

V2 homogenous ListPage

patch

- Added v2 homogenous ListPage model, as discussed on #books-api-design on slack. 

## 0.17.2 ([#32](https://git.mobcastdev.com/Platform/common-spray/pull/32) 2014-10-10 14:46:40)

Upgrade common-json dependency for better error messages 

patch

- Upgraded common-json dependency to get the better error messages from version 0.2.3
- Added test for this behaviour

## 0.17.1 ([#30](https://git.mobcastdev.com/Platform/common-spray/pull/30) 2014-09-30 10:50:56)

Bumping versions

### Improvements

* Bumped common-lang, common-config and common-json

## 0.17.0 ([#29](https://git.mobcastdev.com/Platform/common-spray/pull/29) 2014-09-22 11:32:41)

Placeholder for v2 API json support

### New feature

- Marshaller and unmarshaller for `application/vnd.blinkbox.books.v2+json` media type.

This PR contains bare minimum to get going. We still need to decide what common model classes for paging, error messages, etc. will be in v2 API.

## 0.16.2 ([#28](https://git.mobcastdev.com/Platform/common-spray/pull/28) 2014-09-08 12:57:38)

Dependency updates

Patch to update dependency versions

## 0.16.1 ([#27](https://git.mobcastdev.com/Platform/common-spray/pull/27) 2014-09-05 14:47:41)

Added app version to monitoring/health checks

### Improvements

- Now returns an `X-App-Version` header from health endpoints with the
current version of the service.
- Logs an extra `facilityVersion` into the logging of requests and
responses for the same reason.

## 0.16.0 ([#26](https://git.mobcastdev.com/Platform/common-spray/pull/26) 2014-09-03 17:20:17)

Cross compiles to Scala 2.11, and no Swagger

### Breaking changes

- Removed Swagger v1 dependency and annotations as we’re going to dump
support for this documentation format (we never really implemented it
anyway) and use a YAML-based format for our v2 APIs.

### Improvements

- Now cross-compiles to Scala 2.11

### Deprecations

- `BigDecimalDeserializer` and `ISODateTimeDeserializer` in
`com.blinkbox.books.spray.JsonFormats` are now deprecated and point to
`com.blinkbox.books.spray.unmarshalling` package as these classes have
nothing to do with JSON.

## 0.15.0 ([#25](https://git.mobcastdev.com/Platform/common-spray/pull/25) 2014-08-12 09:25:00)

Added health checks and http bind checking

### New features

- Added a minimal `HttpServer` class which checks that the HTTP bind
succeeded.
- Updated the `HealthCheckHttpService` to have `/health/ping` and
`/health/threads` endpoints like the Codahale metrics ones.

### Improvements

- The health check service now uses its own execution context so it
shouldn’t interfere with the main service.

## 0.14.1 ([#24](https://git.mobcastdev.com/Platform/common-spray/pull/24) 2014-08-07 16:12:21)

Split out the logging of HTTP headers

### Improvements

Interesting HTTP headers are now logged under their own key, e.g.
`httpUserAgent` or `httpXForwardedFor` rather than being lumped
together under `httpRequestHeaders` and `httpResponseHeaders`. This
will enable searches to be done on them more easily.

## 0.14.0 ([#23](https://git.mobcastdev.com/Platform/common-spray/pull/23) 2014-08-06 13:45:43)

Replaced some code with common-json

### Breaking changes

- `JsonFormats`.`ExplicitTypeHints` and
`JsonFormats.ISODateTimeSerializer` have been removed; use the
corresponding classes in `common-json`.

### Bug fixes

- DateTime query parameters are now parsed correctly if they include a
milliseconds component.
- DateTime query parameters are always converted to UTC even if they
were sent in a different time zone.

## 0.13.1 ([#21](https://git.mobcastdev.com/Platform/common-spray/pull/21) 2014-07-25 17:40:19)

Log more info from HTTP requests

### Improvements

- Now captures interesting HTTP request and response headers in the log
output.
- Logs `401 Unauthorized` calls as INFO rather than WARN because this
is a common BAU code for us.

## 0.13.0 ([#17](https://git.mobcastdev.com/Platform/common-spray/pull/17) 2014-06-30 18:58:17)

Added a health check service trait

### New features

- Added a `HealthCheckHttpService` trait to serve Codahale health check results using Spray.
- Added a `rootPath` directive for easier and more reliable hosting of services at configurable paths.

## 0.12.0 ([#20](https://git.mobcastdev.com/Platform/common-spray/pull/20) 2014-07-03 17:28:41)

Quick fix for asQueryParams

### Breaking change

* Changed `asQueryParams` to return Seq[(String, String)]

## 0.11.0 ([#19](https://git.mobcastdev.com/Platform/common-spray/pull/19) 2014-07-03 16:33:23)

Pagination links improvements

### Breaking changes

* Changed the signature of paginated links generation: accepts a sequence of tuples instead of a map, to support repeated parameters

### Improvements

* Added `asQueryParams` for each `SortOrder` object so that you can combine it with pagination.

## 0.10.0 ([#18](https://git.mobcastdev.com/Platform/common-spray/pull/18) 2014-07-02 16:33:10)

Sorting and paging improvements

### Breaking changes

* Added ordered directive
* Added orderedAndPaged directive
* Paging links now support an optional query param
* Added an implicit conversion from `PageLink` to `Link` so that it can be used with `ListPage`

## 0.9.1 ([#16](https://git.mobcastdev.com/Platform/common-spray/pull/16) 2014-06-27 12:47:47)

monitor directive now handles exceptions

### Improvements

- The `monitor` directive now handles any unhandled exceptions using
the default logic so that all requests are logged irrespective or
whether they finish successfully, with a rejection, or with an
exception.

## 0.9.0 ([#15](https://git.mobcastdev.com/Platform/common-spray/pull/15) 2014-06-26 15:49:50)

Diagnostics

### New features

- Added a new `monitor()` directive which adds MDC context about the request and logs basic details of the request and response.
- Added a `clientIP` function to `HttpRequest`.

## 0.8.1 ([#14](https://git.mobcastdev.com/Platform/common-spray/pull/14) 2014-06-20 11:07:06)

ISODateTimeDeserializer

### Improvements

* Added ISODateTimeDeserializer for Joda DateTime query parameters
* Refactored BigDecimalDeserializer tests

## 0.8.0 ([#13](https://git.mobcastdev.com/Platform/common-spray/pull/13) 2014-06-09 10:12:15)

Convert from Java URI/URL to Spray Uri

### New features

- Defines implicit conversions from the Java `URI` and `URL` classes to
a Spray `Uri` instance, which is nicer to work when you’re using the
Spray framework.

## 0.7.2 ([#11](https://git.mobcastdev.com/Platform/common-spray/pull/11) 2014-06-05 12:13:38)

Tiny change to force rebuild, should be published to Artifactory

Patch to update docs, to force a version number increase and rebuild. This is the first version that will be published to Artifactory.

## 0.7.1 ([#9](https://git.mobcastdev.com/Platform/common-spray/pull/9) 2014-06-04 12:22:21)

Removed whitespace

### Patch 

Merged the previous pull request too early :eyes:

## 0.7.0 ([#8](https://git.mobcastdev.com/Platform/common-spray/pull/8) 2014-06-04 12:14:00)

Added BigDecimal deserialiser

### New features

- Added `BigDecimalDeserializer` to allow `BigDecimal` query parameters

## 0.6.0 ([#7](https://git.mobcastdev.com/Platform/common-spray/pull/7) 2014-05-30 12:30:00)

Moved v1 JSON support into its own package

### Breaking changes

- The v1-specific JSON support is now in a `v1` sub-package.

### Improvements

- Includes resource models for v1 paged lists, links, images and errors.
- You can specify `responseTypeHints` on `Version1JsonSupport` for type
hints that are used only on responses (i.e. if you want to ignore the
type hint on requests, which you typically do).

## 0.5.0 ([#6](https://git.mobcastdev.com/Platform/common-spray/pull/6) 2014-05-28 17:38:46)

Added 'do not cache' directives

### New features

- Added `neverCache` and `uncacheable` directives to allow standard ‘do
not cache’ headers to be set.

## 0.4.0 ([#5](https://git.mobcastdev.com/Platform/common-spray/pull/5) 2014-05-23 16:45:47)

Added directive for setting standard cache headers on cached resources

### New features

* Added "cacheable" directive that allows standard cache headers to be set, with a configurable cache expiry time.


## 0.3.0 ([#4](https://git.mobcastdev.com/Platform/common-spray/pull/4) 2014-05-22 14:01:12)

Switched from native JSON library to Jackson

#### New features

- Parses JSON with Jackson instead of native support, as this is generally seen to be faster, hence should be the default choice for our services.

## 0.2.0 ([#3](https://git.mobcastdev.com/Platform/common-spray/pull/3) 2014-05-20 14:55:05)

JSON support + versionable by proteus

#### Breaking changes

- Removed the `version1ResponseHeaders` directive as this is obsoleted
by the `Version1JsonSupport` trait.

#### New features

- Added an `ISODateTimeSerializer` which serialises JodaTime dates
to/from JSON without losing time zone information, which the Json4s
default serialiser does.
- Added a `Version1JsonSupport` trait which can be mixed in to
configure both input and output for the blinkbox books v1 JSON format.

#### Improvements

- Changed the way the version is loaded so it can now be versioned by proteus.

