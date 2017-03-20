# netns - network namespaces in go #

The netns package provides an ultra-simple interface for handling
network namespaces in go. Changing namespaces requires elevated
privileges, so in most cases this code needs to be run as root.

## Local Build and Test ##

You can use go get command:

    go get github.com/vishvananda/netns

Testing (requires root):

    sudo -E go test github.com/vishvananda/netns

## Example ##

```go
package main

import (
    "net"
    "runtime"
    "github.com/vishvananada/netns"
)

func main() {
    // Lock the OS Thread so we don't accidentally switch namespaces
    runtime.LockOSThread()
    defer runtime.UnlockOSThread()

    // Save the current network namespace
    origns, _ := netns.Get()
    defer origns.Close()

    // Create a new network namespace
    newns, _ := netns.New()
    defer newns.Close()

    // Do something with tne network namespace
    ifaces, _ := net.Interfaces()
    fmt.Printf("Interfaces: %v\n", ifaces)

    // Switch back to the original namespace
    netns.Set(origns)
}

```
This project is clone from https://github.com/OpenSnaproute/netns.git 
This project is only for learing purpose.
This project is assumed to be changed by a program. 
DONOT CHECKOUT OR CLONE THIS PROJECT
