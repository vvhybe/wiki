---

### `display-protocols.md`

```markdown
# 🖥️ Display Protocols: Xserver vs Wayland

## Overview
Display protocols determine how graphical applications interact with the hardware. The two most common protocols are **Xserver (X11)** and **Wayland**.

---

## Xserver (X11)

- **History**: Developed in 1984, widely used for decades.
- **Architecture**:
  - Client-server model.
  - The X server manages input/output devices and displays.
  - Clients (applications) send requests to the server.
- **Features**:
  - Mature ecosystem with broad compatibility.
  - Extensive support for legacy applications.
  - Network transparency (remote desktops).
- **Drawbacks**:
  - Complex and outdated architecture.
  - Security concerns due to its age.
  - Higher latency compared to Wayland.

---

## Wayland

- **History**: Introduced in 2008 as a modern alternative to X11.
- **Architecture**:
  - Direct communication between clients and the compositor.
  - Simplified protocol with fewer abstractions.
- **Features**:
  - Improved performance and lower latency.
  - Enhanced security (no root access for display servers).
  - Better support for modern hardware (e.g., HiDPI, touchscreens).
- **Drawbacks**:
  - Limited support for legacy applications.
  - Some tools and features may not yet be fully compatible.

---

## Key Differences
| Feature               | Xserver (X11)                     | Wayland                          |
|-----------------------|-----------------------------------|----------------------------------|
| **Performance**       | Higher latency                   | Lower latency                    |
| **Security**          | Less secure                      | More secure                      |
| **Compatibility**     | Broad (legacy apps)              | Limited (modern apps)            |
| **Remote Desktops**   | Native support                   | Requires additional tools        |
| **Architecture**      | Client-server model              | Direct client-compositor model   |

---

## Choosing Between Xserver and Wayland

- **Use Xserver if**:
  - You rely on legacy applications.
  - You need network transparency (remote desktops).
- **Use Wayland if**:
  - You prioritize performance and security.
  - You use modern hardware (e.g., HiDPI displays, touchscreens).

---

## NixOS Integration
In NixOS, you can configure your display protocol in `configuration.nix`:

```nix
services.xserver.enable = true; # For Xserver
services.wayland.enable = true; # For Wayland