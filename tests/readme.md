# Run the checks

From the repository root run `python "tests/build tests.py"`, then run these with the standalone Luau interpreter on PATH

```text
luau "tests/generated/search tests.luau"
luau "tests/generated/reachability tests.luau"
```

Expected outputs are `baseline=960 additional=1182 dispatches=11` and `reachability=7382`. Deadline-based scheduling can change the dispatch count and its associated assertion count on a slower machine. Generated files are ignored and extracted from the current main source

The baseline uses an independent exhaustive shortest-path reference. Additional search assertions cover immutable snapshots, charged pops, sliced costs, deadlines, fairness, generations, compatibility and the open/closed passage comparison. Reachability uses independent queue traversal on seeded rectangular maps. The command-line suite uses a fixed PRNG substitute and mock attribute adapters; it does not simulate Roblox physics

## Studio fixtures

The [cycle server](cycle%20server.luau) and [cycle client](cycle%20client.luau) fixtures check all 15 arrivals, eight ordered collapses, 96 chunks, 144 fragments, 630 dots, shared rerouting, a physically crossed cheaper shortcut and replay startup. Two independent clients must observe upright rigs, probe colors, the HUD and camera

The [lifetime server](lifetime%20server.luau) and [lifetime client](lifetime%20client.luau) fixtures require two rigs moving horizontally faster than one stud per second before each live, detached and destroyed shutdown case. They check movement, active owned resources and the original rotation settings. Live shutdown also checks stopped and offline states. Unexpected owner loss leaves the last cached attributes; an explicitly held detached Script keeps inactive children until destroyed

These are StudioTestService harnesses, not production scripts or automatic place importers. They require a temporary copied `candidatefixture`, copied HUD/camera, test event names and a disabled `candidatecontroller` under ServerScriptService. The test controller uses exactly three namespace substitutions to address the copied world and events. Full integration cannot be reproduced from this repository without the authored assets

Use the cycle server argument `single cycle` with two clients and the lifetime server argument `final lifetime`. Both server fixtures assert place ID `113425488924507`. Check the fixture and controller are correctly isolated before running them; they disable other server Scripts in the test session

Remove test fixtures and harnesses after testing. This source copy includes the checks, not historical result reports. Building the command-line tests does not run the Studio fixtures or publish the place
