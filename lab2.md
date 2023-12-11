1. **Create a script that asks for user name then sends a greeting to him.**
   ![](/pics/VirtualBoxVM_RGlYNpezen.png) ![](/pics/VirtualBoxVM_RnqzKEE7pJ.png)
2. **Create a script called `s1` that calls another script `s2` where:**
   a. In `s1`, there is a variable called `x` with a value of 5.
   b. Try to print the value of `x` in `s2` by two different ways.
   ![](/pics/VirtualBoxVM_Mw9mbGqjD2.png) ![](/pics/VirtualBoxVM_euY6P675xp.png) ![](/pics/VirtualBoxVM_zS6YKlEzMS.png)
3. **Create a script called `mycp` where:**
   a. It copies a file to another.
   b. It copies multiple files to a directory.

```bash
#!/bin/bash

if [ $# -lt 2 ]; then
  echo "Usage: ./mycp <source> <destination>"
  exit 1
fi

destination="${!#}"

if [ -d "$destination" ]; then
  for source in "$@"; do
     if [ "$source" = "$destination" ]; then
	continue
     fi
   cp "$source" "$destination"
  done
else
   source="$1"
   destination="$2"
   cp "$source" "$destination"
fi

if [ $? -eq 0 ]; then
 echo "File(s) copied successfully."
else
 echo "Error: Failed to copy file(s)."
fi
```

![](/pics/VirtualBoxVM_BF9U07S1Cu.png)

4. **Create a script called `mycd` where:**
   a. It changes the directory to the user's home directory if it is called without arguments.
   b. Otherwise, it changes the directory to the given directory.

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
  cd ~
elif [ -d "$1" ]; then
  cd "$1"
else
  echo "Usage: ./mycd <directory>"
fi
echo "Current directory: $PWD"
```

![](/pics/VirtualBoxVM_QjY6E6CT81.png)

5. **Create a script called `myls` where:**
   a. It lists the current directory if it is called without arguments.
   b. Otherwise, it lists the given directory.

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
ls
elif [ -d "$1" ]; then
ls "$1"
else
echo "Usage: ./myls [directory]"
fi
```

![](/pics/VirtualBoxVM_CNhJJRuBPu.png)

6. **Enhance the above script to support the following options individually:**
   a. `--l`: list in long format.
   b. `--a`: list all entries, including hidden files.
   c. `--d`: if an argument is a directory, list only its name.
   d. `--i`: print inode number.
   e. `--R`: recursively list subdirectories.

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
  ls
elif [ $# -eq 1 ] || [ $# -eq 2 ]; then
  option=""
  directory=""

  case "$1" in
    -l) option="-l" ;;
    -a) option="-a" ;;
    -d) option="-d" ;;
    -i) option="-i" ;;
    -R) option="-R" ;;
    *)  directory="$1";;
  esac

  if [ $# -eq 1 ] && [ -d "$1" ]; then
   ls "$directory"
   exit 1
  elif [ $# -eq 1 ] && [ -n "$option" ]; then
   ls $option
   exit 1
  fi

  if [ $# -eq 2 ]; then
    directory="$2"
  fi

  if [ -d "$directory" ] && [ $# -eq 2 ]; then
    ls $option "$directory"
  else
    echo "Error: '$directory' is not a directory."
  fi
else
  echo "Usage: $0 [-l | -a | -d | -i | -R] [directory]"
fi
```

![](/pics/VirtualBoxVM_CS9OFiIv8m.png)
