This is a fork of badunk/js-fixtures  
I'm using a `<div>` container as a sandbox instead of an `<iframe>` and I changed the default path for fixtures
to `./fixtures/`

## Installation

Download the raw from github.

You may also load it using AMD with `require('fixtures')`

## Usage

Use `fixtures.load('your-fixture.html')` in your specs.

Clean up fixtures with `fixtures.cleanUp()` (perhaps in a `afterEach()` block)

## Fixtures

Fixture module allows you to load HTML content to be used by your tests.
    
By default, fixtures are loaded from `./fixtures/`. You can configure this path: `fixtures.path = 'my/new/path';`.

Your fixture is being loaded into a div container that is automatically added to the DOM (If you _REALLY_ must change id of this container, try: `fixtures.containerId = 'my-new-id';` in your test runner). To make tests fully independent, make sure to clean up after your fixtures with `fixtures.cleanUp`. Also, fixtures are internally cached, so you can load the same fixture file in several tests without penalty to your test suite's speed.
    
Several methods for loading fixtures are provided:

- `load(fixtureUrl[, fixtureUrl, ...])`
  - Loads fixture(s) from one or more files and automatically appends them to the DOM (to the fixtures container).
- `appendLoad(fixtureUrl[, fixtureUrl, ...])`
  - Same as load, but adds the fixtures to the pre-existing fixture container.
- `read(fixtureUrl[, fixtureUrl, ...])`
  - Loads fixture(s) from one or more files but instead of appending them to the DOM returns them as a string (useful if you want to process fixture's content directly in your test).
- `set(html)`
  - Doesn't load fixture from file, but instead gets it directly as a parameter. Automatically appends fixture to the DOM (to the fixtures container). It is useful if your fixture is too simple to keep it in an external file or is constructed procedurally, but you still want Fixture module to automatically handle DOM insertion and clean-up between tests for you.
- `appendSet(html)`
  - Same as set, but adds the fixtures to the pre-existing fixture container.
- `preload(fixtureUrl[, fixtureUrl, ...])`
  - Pre-loads fixture(s) from one or more files and stores them into cache, without returning them or appending them to the DOM. All subsequent calls to `load` or `read` methods will then get fixtures content from cache, without making any AJAX calls (unless cache is manually purged by using `clearCache` method). Pre-loading all fixtures before a test suite is run may be useful when working with libraries like jasmine-ajax that block or otherwise modify the inner workings of JS or jQuery AJAX calls.

Additionally, two clean up methods are provided:

- `clearCache()`
  - purges Fixture module internal cache (you should need it only in very special cases; typically, if you need to use it, it may indicate a smell in your test code)
- `cleanUp()`
  - cleans-up fixtures container


## Executing Tests
Do an `npm install` to grab the test dependencies.  Then point your browser to the index.html file.

## Cross domain policy problems under Chrome

Newer versions of Chrome don't allow file:// URIs read other file:// URIs. In effect, js-fixtures cannot properly load fixtures under some versions of Chrome. An override for this is to run Chrome with a switch `--allow-file-access-from-files`.  Another way is to ensure that you are executing the test runner under a web server.
