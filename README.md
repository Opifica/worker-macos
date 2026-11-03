# worker-macos

The **macOS worker** for [Opifica](https://github.com/opifica): it runs on macOS build machines and runs every job
in a fresh VM using **Apple Virtualization.framework**.

> **Status:** early development. See the [organisation page](https://github.com/opifica) for the architecture.

## What it does

- Connects out to the Opifica controller over gRPC + mTLS (no inbound ports needed)
- Keeps a warm pool of pre-booted VMs cloned from signed golden images
- Hands each job a fresh VM, then destroys it when the job finishes
- Serves the repository from a local Git mirror and passes runtime secrets to the guest agent

All of this, apart from the hypervisor driver, comes from the shared worker kit in
[`opifica/pkg/worker`](https://github.com/opifica/opifica). This repository contains only the macOS-specific code.

## Requirements

- Apple silicon Mac
- Apple's licence allows at most **2 macOS VMs per Mac**, so each machine runs at most 2 jobs in parallel
- Built on macOS with cgo, and signed with the `com.apple.security.virtualization` entitlement

## License

[EUPL-1.2](LICENSE)
