# Problem

How to find which Display Server is running: Wayland or X11

# Solution

[This answer](https://unix.stackexchange.com/questions/202891/how-to-know-whether-wayland-or-x11-is-being-used) lists the steps:

- Obtain the session ID to pass in by issuing:
`loginctl`
- Then:
`loginctl show-session <SESSION_ID> -p Type`
- Use the one corresponding to your user name.

Refer to: https://fedoraproject.org/wiki/How_to_debug_Wayland_problems

So, for me it is:
```bash
$ loginctl show-session 2 -p Type                                                  
Type=wayland
```

# Alternative Solution
Run
```
echo $XDG_SESSION_TYPE
```
