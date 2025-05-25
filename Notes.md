
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
