# Problem

An outdated repo is still being sync'ed and checked every time Fedora's `dnf` runs. How to remove it?

# Solution

Before removing a repo, make sure no apps are still installed from that repo.
```bash
dnf repo-pkgs <repoid> list installed
```

The folder `/etc/yum.repos.d/` lists all repos. Each repo is just a file with `.repo` extension. By deleting the file, it's removed from the list.  
Also, by simply renaming the file to `.old` extension, it's removed from the list.  