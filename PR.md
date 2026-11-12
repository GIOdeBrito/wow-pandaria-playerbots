Add portable Linux x86-64 build to CI pre-release.

The existing Linux build compiles with `-march=native`, `BUILD_DEPLOY=1` default, so binaries built on current GitHub runners carry host CPU instructions and fail with "Illegal instruction" (instruction AVX512 at `je_bin_shard_sizes_boot()`, tested with gdb) on x86-64 hosts.

Adds `.github/workflows/linux-x86_64.yml` (baseline `x86-64` via `-DBUILD_DEPLOY=0`) alongside the existing host-tuned `linux_gcc.yml` build. Wires it into `beta-prerelease.yml` so the daily `ci-playerbot-beta` pre-release publishes both `ci-linux-x64.zip` and `ci-linux-x86_64.zip`.
