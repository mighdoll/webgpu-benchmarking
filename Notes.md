
# Notes on exploring the library

## new packaged install

install:

```sh
git clone webgpu-benchmarking
pnpm install
```

run node benchmark:

```sh
pnpm bench:node
```

## Command line snippet to trace metal performance

original
```sh
METAL_CAPTURE_ENABLED=1 DAWN_TRACE_FILE_BASE=/Users/jdowens/Downloads/ xctrace record --output name-of-trace-file.trace --template "CPU Profiler" --time-limit 10s --launch -- /Users/jdowens/.nvm/versions/node/v23.0.0/bin/node benchmarking_node.mjs
```

locally modified:
```sh
METAL_CAPTURE_ENABLED=1 DAWN_TRACE_FILE_BASE=/tmp xctrace record --output /tmp/trace1.trace --template "Metal System Trace" --time-limit 10s --launch -- /opt/homebrew/bin/node benchmarking_node.mjs
```

Seems to only record the entire time of a vertex/fragment/compute pass. Seems similar to what we can get from the webgpu api already, but 'Instruments' is a nice graphical viewer..

I wonder if there's a way to get more details (like occupancy) by using the metal debugger: https://developer.apple.com/documentation/xcode/analyzing-apple-gpu-performance-using-a-visual-timeline

# Running in browser tests

With some tweaks to the html/script loading, I can run a local webserver in `webgpu-benchmarking` via `python3 -m http.server 8000`.

(there's some code in there to produce graphs when running via node too which I didn't figure out how to run)

Once that's done, https://localhost:8000 loads the benchmarking page.
Manually edit benchmarking.mjs to enable different test suites.

Many of the suites report errors in the browser console.
I'm not sure what's supposed to work, but some suites make pretty graphs via observable.

And https://localhost:8000/standalone.html loads the standalone test page.

