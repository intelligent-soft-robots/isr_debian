isr_debian
----------

Creating a debian install file from a colcon/ament install folder.

beta version: very limited capacities. Assumes python3.6, and install only libraries and python packages (no executable nor configuration file)

# installation

```bash
# assumes python3
pip install isr_debian
```

# usage

- In at least one of your ament package, host a file path_to_package_src/debian/control. Exemple of content:

```
Package: my_package
Version: 1.00-1
Section: base
Priority: optional
Architecture: amd64
Depends: libboost-all-dev, my_other_apt_dependency
Maintainer: MySurname MyLastname <myname@myorganization.com
Description: my_package, and what it does
```

- In the CMakeLists.txt of the package, set this file for installation:

```cmake
install(FILES debian/control DESTINATION debian)
```

- Compile your workspace as usual

- Go the the workspace folder (i.e. the root folder of the install folder) and call:

```bash
isr_make_debian
```

If all goes well, a debian file should have been created in the current directory.

You may proceed with installation via:

```
sudo apt install ./path_to_deb_file
```