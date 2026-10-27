## What happens

When granting a Bot access to a folder, the directory picker stalls: after choosing a drive (`D:\`), the file list stays on skeleton placeholders for several minutes before populating. CPU and memory are not saturated (user checked Task Manager), so this is not resource exhaustion.

The dialog offers drive tabs (home, C:, D:, E:, F:, Z:), a path input with a "go" button, the folder list, and a "show hidden folders" toggle; the delay is in listing.

## Expected

- List directories incrementally or paginate, and show progress instead of an empty skeleton.
- Entering a path directly should never wait on a full directory scan.

## Suspected cause (unverified)

The picker enumerates an entire directory level synchronously and possibly reads metadata or icons per entry; slow disks, network shares, or directories lacking permissions would multiply the cost.

## Workaround

Paste the full path into the path box and press go, then pick the folder there — this bypasses the slow listing.

## Impact

Granting access is a required setup step; a multi-minute freeze reads as a hang, and combined with silently narrowed permissions it easily makes users give up on configuring access.

Reported 2026-10-27 from a community group; App version and disk type not captured.
