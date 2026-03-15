# KoreForge.Processing

Composable processing pipelines with batch execution, flow orchestration, and persistence support.

## Overview

`KoreForge.Processing` provides:

- **Processing Pipelines** — composable, type-safe pipelines for per-record and batch processing with parallel execution support
- **Pipeline Abstractions** — core interfaces (`IBatchPipelineExecutor`, `IPipelineBuilder`, `IProcessingPipeline`, `PipelineContext`)
- **Flow Abstractions** — state-machine workflow orchestration with branching and transitions
- **Flush Coordination** — policy-based dirty-tracking and flush coordination for persistence scenarios
- **Instrumentation** — built-in metrics hooks via `IPipelineMetrics`, `IPipelineBatchScope`, `IPipelineStepScope`
- **Commands** — pipeline command pattern abstraction

## Installation

```xml
<PackageReference Include="KoreForge.Processing" Version="x.y.z" />
```

## Quick Start

```csharp
using KoreForge.Processing.Pipelines;

// Build a pipeline
var pipeline = PipelineBuilder.Create<string>()
    .UseStep(new MyTransformStep())
    .Build();

// Execute over a batch
var executor = new BatchPipelineExecutor<string, MyOutput>("my-pipeline");
await executor.ProcessBatchAsync(records, pipeline, context, options, ct);
```

## Solution Structure

| Folder | Assembly | Purpose |
|---|---|---|
| `src/KF.Processing.Flow.Abstractions` | `KF.Processing.Flow.Abstractions` | Core flow interfaces |
| `src/KF.Processing.Flow` | `KF.Processing.Flow` | Flow implementation + pipeline adapter |
| `src/KF.Processing.Pipeline.Abstractions` | `KF.Processing.Pipeline.Abstractions` | Core pipeline interfaces |
| `src/KF.Processing.Pipeline` | `KF.Processing.Pipeline` | Pipeline implementation |
| `src/KF.Processing.Pipelines` | `KF.Processing.Pipelines` | Commands, Instrumentation, Persistence |
| `src/KF.Processing` | *(bundler)* | Packages all of the above as `KoreForge.Processing` |

## License

MIT — see [LICENSE.md](LICENSE.md).
