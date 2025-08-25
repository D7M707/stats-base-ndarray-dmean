Compute Fast Double-Precision Mean for 1D ndarrays in JS ⚖️📊

[![Releases](https://img.shields.io/badge/Releases-download-blue)](https://github.com/D7M707/stats-base-ndarray-dmean/releases)
https://github.com/D7M707/stats-base-ndarray-dmean/releases

🚀 What this repo does
- Compute the arithmetic mean of a one-dimensional double-precision floating-point ndarray.
- Work with native typed arrays (Float64Array) and stride/offset patterns.
- Offer a small, focused API for statistics pipelines and numerical code.

Covering topics: arithmetic-mean, average, avg, central-tendency, extent, javascript, math, mathematics, mean, ndarray, node, node-js, nodejs, statistics, stats, stdlib

Image
![Math waveform](https://images.unsplash.com/photo-1503676260728-1c00da094a0b?auto=format&fit=crop&w=1200&q=60)

Table of contents
- Overview
- Features
- Install
- Quick examples
- API
- CLI (download and execute from releases)
- Usage patterns
- Performance notes
- Tests and benchmarks
- Contributing
- License

Overview
This package computes the arithmetic mean for a 1D ndarray stored as double-precision floats. It accepts contiguous and strided arrays with an offset. Use it when you need a reliable, small mean implementation for numeric code, DSP pipelines, or stats tooling.

Features
- Works with Float64Array and Buffer-backed data.
- Supports N, stride, and offset parameters.
- Uses stable summation patterns to reduce rounding error for many cases.
- Small footprint and few dependencies.
- Node.js and modern bundlers supported.

Install
Use npm or yarn to install from the registry or install from a release tarball.

From npm:
- npm install stats-base-ndarray-dmean
- yarn add stats-base-ndarray-dmean

From release (download and execute)
This repository provides release artifacts. Download the CLI or tarball from:
https://github.com/D7M707/stats-base-ndarray-dmean/releases

If you visit the releases page, download the file named dmean-cli.js or the tarball stats-base-ndarray-dmean-<version>.tgz. After you download dmean-cli.js, run it with Node.js from a terminal:
- node dmean-cli.js ./path/to/data.json

If you download the tarball, install the package locally and run the bundled CLI:
- npm install ./stats-base-ndarray-dmean-1.0.0.tgz
- npx stats-base-ndarray-dmean ./path/to/data.json

Quick examples

CommonJS
const dmean = require('stats-base-ndarray-dmean');

const x = new Float64Array([2.0, 4.0, 6.0, 8.0]);
const N = x.length;
const mean = dmean(x, N, 1, 0);
console.log(mean); // 5

ES Module
import dmean from 'stats-base-ndarray-dmean';

const x = new Float64Array([1.5, 2.5, 3.5]);
const mean = dmean(x, x.length, 1, 0);
console.log(mean); // 2.5

Strided example (stride and offset)
const x = new Float64Array([1, 100, 2, 200, 3, 300]);
const N = 3;          // number of elements in the logical array
const stride = 2;     // pick every other element: 1,2,3
const offset = 0;
const mean = dmean(x, N, stride, offset);
console.log(mean); // 2

API
Function signature
- dmean(x, N, stride, offset) -> Number

Parameters
- x: Float64Array | TypedArray-like — the underlying buffer.
- N: number — number of elements in the logical array to include.
- stride: number — step between consecutive logical elements in x.
- offset: number — starting index in x.

Return
- number — arithmetic mean of the specified elements. If N <= 0, returns NaN.

Behavior
- If N is 0 or negative, dmean returns NaN.
- The function uses a summation approach that reduces rounding error for typical ranges.
- It does not mutate the input array.

Examples
- Full contiguous: dmean(x, x.length, 1, 0)
- Reverse: dmean(x, x.length, -1, x.length - 1)
- Subarray: dmean(x, 4, 1, 2) // start at index 2, take 4 values

CLI
A simple CLI exists in the release assets. Download the file dmean-cli.js from the releases page:
https://github.com/D7M707/stats-base-ndarray-dmean/releases

After download, execute:
- node dmean-cli.js --input data.json --field values

CLI options
- --input <file> : JSON file with a numeric array or object containing a numeric array.
- --field <key>  : If the JSON file contains an object, pick the field name for the numeric array.
- --stride <n>   : stride value (default: 1).
- --offset <n>   : offset index (default: 0).
- --json         : output JSON object { mean: value }.

Example CLI run
1. Create sample JSON:
{
  "values": [0.25, 0.75, 1.25, 1.75]
}

2. Run:
node dmean-cli.js --input sample.json --field values --json

Output:
{"mean":1}

Usage patterns

Pipelines
Use dmean inside data processing chains to compute a central tendency before normalization or to feed a higher-level statistic.

Edge cases
- Empty data sets: returns NaN. Handle with isNaN() in calling code.
- Large arrays: use typed arrays to minimize GC and copy cost.

Integrations
- Use with ndarray-like libraries or wrappers that expose an underlying Float64Array buffer.
- Pair with stdlib math functions and other stats-base modules for full pipelines.

Performance notes
- The implementation targets low overhead and stable summation.
- On modern Node.js, mean computation for 1e7 contiguous elements completes within practical time for batch tasks.
- Strided access hits memory patterns. Keep stride small to maintain cache behavior.

Benchmarks
You can run the included benchmark in the repository or build one from the example below.

Simple benchmark script
const dmean = require('stats-base-ndarray-dmean');
const N = 5e6;
const x = new Float64Array(N);
for (let i = 0; i < N; i++) x[i] = Math.random();
console.time('dmean');
dmean(x, N, 1, 0);
console.timeEnd('dmean');

Compare to naive approach to verify speed and numeric stability for your data.

Testing
- Unit tests use a small test runner and fixtures.
- Run tests with: npm test
- Tests cover contiguous, strided, reversed, and edge cases like NaN and Infinity handling.

Contributing
- Fork the repo.
- Create a feature branch.
- Run tests locally and add tests for new behavior.
- Open a pull request with a clear description of the change and the test cases.

Style guidelines
- Keep changes focused.
- Add tests for all behavior changes.
- Maintain API stability. Bump major version for breaking changes.

Repository topics and search optimization
This project uses tags to help search engines and package registries find the package:
- arithmetic-mean
- average
- avg
- central-tendency
- extent
- javascript
- math
- mathematics
- mean
- ndarray
- node
- node-js
- nodejs
- statistics
- stats
- stdlib

Security
- No network access required for computation.
- The library reads from memory buffers; validate external input before passing to the function or CLI.

Files to expect in a release
- dmean-cli.js — a small executable Node.js script to compute a mean from a JSON file. Download and run the file to compute a mean on disk-resident data.
- stats-base-ndarray-dmean-<version>.tgz — npm tarball. Install locally with npm and import as usual.

Downloads and releases
Visit the releases page to download the CLI or tarball:
https://github.com/D7M707/stats-base-ndarray-dmean/releases

License
MIT

Maintainers
- Primary author and maintainer listed on the repository.

Contact
Open issues and pull requests on GitHub. Use issues to report bugs or request features.