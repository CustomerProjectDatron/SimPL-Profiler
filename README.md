# Profiler Viewer

A zero-dependency, single-file HTML profiler viewer that runs entirely in the browser.
Load any JSON profiling trace by drag & drop or file picker — no server, no install required.

![Profiler Viewer screenshot](screenshot.png)

## Features

| Tab | Description |
|---|---|
| **⬡ Baum** (Tree) | Collapsible call tree with time bars, self-time overlay and call-count badges. Lazy DOM rendering handles 50 MB+ files smoothly. |
| **⬥ Hotspots** | Aggregated method list, sortable by total time, self time or call count. Shows average time per call. |
| **🔥 Flame Graph** | Canvas-based flame graph. Click any block to zoom in; use *Back* / *Reset* to navigate. Hover for tooltip. |
| **↩ Bottom-up** | Every method listed with its callers. Searchable and sortable. |

## SimPL example

The following SimPL module shows how to enable the profiler, run your code, and write the result to a JSON file:

```simpl
module test

import LinearAlgebraHelper
using Profiler
import Base
import File

export program Main
    EnableProfiler
    Do
    File::FileWrite(
        filename="Profile.json"
        value<-Base::ValueToJson("Profile", GetProfilerResult)
    )
endprogram

program Do
    Something
endprogram

program Something
    for i from 0 to 100
        _result_ = LinearAlgebraHelper::AbsPosition(LinearAlgebraHelper::NewPos(1, 2, 3))
    endfor
endprogram

end
```

The generated `Profile.json` can be loaded directly into this viewer via drag & drop.

> For the JSON trace format specification see [TECH_DOC.md](TECH_DOC.md).

## License

MIT
