# Verify AddControllers default assembly

## Context

`src/CCSWE.nanoFramework.WebServer/WebServer/Bootstrapper.cs:89`: `AddControllers()` with no assembly falls back to `Assembly.GetExecutingAssembly()`. That call runs inside the WebServer library, so it may return the library rather than the app, and app controllers might not be discovered. Owner believes it works.

Emily.Clock (`device/Emily.Clock/Bootstrapper.cs`) passes `typeof(Bootstrapper).Assembly`, so it doesn't exercise the default.

## Steps

Recommended: make `assembly` required (breaking: needs a WebServer major version bump), update `src/CCSWE.nanoFramework.WebServer/README.md`, and delete this file. Parked until the repo's versioning is settled.

Alternative, without a breaking change:

1. On a device or emulator, run a sample app that calls `AddControllers()` without an assembly (e.g. uncomment `services.AddControllers();` in `samples/Samples.CCSWE.nanoFramework.WebServer/Program.cs`) and confirm its controllers are registered.
2. If they aren't, fix it and update the README.
3. Delete this file.
