# DISCLAIMER
Your warranty is now void. I am not responsible for any damage to your device.
Use this kernel at your own risk.

# Overview
This is a kernel fork for LineageOS 18.1 (guacamole) with patches for enabling Docker/LXC support with cgroups v1.

- Rootful Docker: Supported on cgroup v1.
- Rootless Docker: Runs, but cgroup-based resource limits do not work on cgroup v1.
- cgroups v2: Not supported by device.

A Magisk patch is required, not included into releases.

On boot, you may see: "There's an internal problem with your device." This is expected for modified kernels.

# Supported Docker Setups (cgroups v1)


### DroidSpaces -> Docker (Rootful)
- Status: Works on Supported Releases, Recommended #1
- Supported **starting from kernel release v1.2 and newer**
- Requires devtmpfs flags enabled (added in v1.2)
- IMPORTANT: "Manual deadlock shield" should be disabled when configuring the container. Otherwise, Docker and Systemd sandboxing will not work.
- Works with DroidSpaces-OSS:
  https://github.com/ravindu644/Droidspaces-OSS
- Link to kernel release: **[Release 1.2 (LOS 18.1)](https://github.com/M1DNYT3/android_kernel_oneplus_sm8150_lxc_docker/releases/tag/18.1-LXC-1.2-Stable)**

## LXC -> Docker (Rootful)
- Status: Works on all releases, Recommended #2
- Requirements: privileged LXC, security.nesting=true, AppArmor relaxed (lxc.apparmor.profile=unconfined)  
- Storage driver: overlay2 or fuse-overlayfs

## LXC -> Docker (Rootless)
- Status: Limited  
- Notes: Runs, but no cgroup limits on v1

## chroot -> Docker (Rootful)
- Status: Works  
- Requirements: namespaces, cgroup v1 controllers, networking, overlayfs/fuse-overlayfs

## chroot -> Docker (Rootless)
- Status: Limited  
- Notes: No cgroup limits; additional manual setup required

## Termux (native root, not proot) -> Docker
- Rootful: Works  
- Rootless: Limited (no cgroup limits)

## Termux (proot) -> Docker
- Not supported

# Optional LXC Module
A ready-to-use LXC Magisk module exists:
https://github.com/tomxi1997/lxc-magisk-modules-for-android-/releases

The module is in Chinese; review and translate the installation log.
