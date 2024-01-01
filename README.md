<!--

@license Apache-2.0

Copyright (c) 2018 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# trycatchAsync

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> If a function does not return an error, invoke a callback with the function result; otherwise, invoke a callback with a value `y`.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->



<section class="usage">

## Usage

```javascript
import trycatchAsync from 'https://cdn.jsdelivr.net/gh/stdlib-js/utils-async-try-catch@deno/mod.js';
```

#### trycatchAsync( x, y, done )

If a function `x` does not return an error, invokes a `done` callback with the function result; otherwise, invokes a `done` callback with a value `y`.

```javascript
import randu from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-base-randu@deno/mod.js';

function x( clbk ) {
    setTimeout( onTimeout, 0 );
    function onTimeout() {
        if ( randu() > 0.5 ) {
            return clbk( null, 1.0 );
        }
        clbk( new Error( 'oops' ) );
    }
}

function done( error, result ) {
    if ( error ) {
        console.log( error.message );
    }
    console.log( result );
}

trycatchAsync( x, -1.0, done );
```

The function `x` is provided a single argument:

-   `clbk`: callback to invoke upon function completion

The callback accepts two arguments:

-   `error`: error object
-   `result`: function result

The `done` callback is invoked upon function completion and is provided two arguments:

-   `error`: error object
-   `result`: either the result of `x` or the provided value `y`

If the function `x` does not return a truthy `error` argument, the `error` argument provided to the `done` callback is `null`. If `x` does return a truthy `error` argument, the `done` callback is invoked with both the `error` and the provided value `y`.

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

## Notes

-   Execution is **not** guaranteed to be asynchronous. To guarantee asynchrony, wrap the `done` callback in a function which either executes at the end of the current stack (e.g., `nextTick`) or during a subsequent turn of the event loop (e.g., `setImmediate`, `setTimeout`).

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import randu from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-base-randu@deno/mod.js';
import trycatchAsync from 'https://cdn.jsdelivr.net/gh/stdlib-js/utils-async-try-catch@deno/mod.js';

var i;

function next() {
    trycatchAsync( x, 'beep', done );
}

function x( clbk ) {
    setTimeout( onTimeout, 0 );
    function onTimeout() {
        if ( randu() > 0.9 ) {
            return clbk( null, 'BOOP' );
        }
        clbk( new Error( 'oops' ) );
    }
}

function done( error, result ) {
    if ( error ) {
        console.log( error.message );
    }
    i += 1;
    console.log( result );
    if ( i < 100 ) {
        return next();
    }
}

i = 0;
next();
```

</section>

<!-- /.examples -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/utils-try-catch`][@stdlib/utils/try-catch]</span><span class="delimiter">: </span><span class="description">if a function does not throw, return the function return value; otherwise, return `y`.</span>
-   <span class="package-name">[`@stdlib/utils-async/try-then`][@stdlib/utils/async/try-then]</span><span class="delimiter">: </span><span class="description">if a function does not return an error, invoke a callback with the function result; otherwise, invoke a second function.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2024. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/utils-async-try-catch.svg
[npm-url]: https://npmjs.org/package/@stdlib/utils-async-try-catch

[test-image]: https://github.com/stdlib-js/utils-async-try-catch/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/utils-async-try-catch/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/utils-async-try-catch/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/utils-async-try-catch?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/utils-async-try-catch.svg
[dependencies-url]: https://david-dm.org/stdlib-js/utils-async-try-catch/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/utils-async-try-catch/tree/deno
[umd-url]: https://github.com/stdlib-js/utils-async-try-catch/tree/umd
[esm-url]: https://github.com/stdlib-js/utils-async-try-catch/tree/esm
[branches-url]: https://github.com/stdlib-js/utils-async-try-catch/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/utils-async-try-catch/main/LICENSE

<!-- <related-links> -->

[@stdlib/utils/try-catch]: https://github.com/stdlib-js/utils-try-catch/tree/deno

[@stdlib/utils/async/try-then]: https://github.com/stdlib-js/utils-async-try-then/tree/deno

<!-- </related-links> -->

</section>

<!-- /.links -->
