1. **Create a script that asks for user name then sends a greeting to him.**<br/>
   ![](/pics/VirtualBoxVM_RGlYNpezen.png)
   ![](/pics/VirtualBoxVM_RnqzKEE7pJ.png)
2. **Create a script called `s1` that calls another script `s2` where:**
   - In `s1`, there is a variable called `x` with a value of 5.
   - Try to print the value of `x` in `s2` by two different ways.<br/>
     ![](/pics/VirtualBoxVM_Mw9mbGqjD2.png)
     ![](/pics/VirtualBoxVM_euY6P675xp.png)
     ![](/pics/VirtualBoxVM_zS6YKlEzMS.png)
3. **Create a script called `mycp` where:**
   - It copies a file to another.
   - It copies multiple files to a directory.

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
   - It changes the directory to the user's home directory if it is called without arguments.
   - Otherwise, it changes the directory to the given directory.

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
   - It lists the current directory if it is called without arguments.
   - Otherwise, it lists the given directory.

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
   - `--l`: list in long format.
   - `--a`: list all entries, including hidden files.
   - `--d`: if an argument is a directory, list only its name.
   - `--i`: print inode number.
   - `--R`: recursively list subdirectories.

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

Bonus: enhance the above script to support the following Synopsis:

- myls -option1 –option2
- myls –option2 –option1
- myls –option1option2
- myls –option2option1

```bash
#!/bin/bash

function help {
    echo "Usage: ./myls [OPTIONS] [DIRECTORY]"
    echo "List information about files and directories."
    echo ""
    echo "Options:"
    echo "  -l    List in long format"
    echo "  -a    List all entries, including hidden files"
    echo "  -d    If a directory, list only its name"
    echo "  -i    Print inode number"
    echo "  -R    Recursively list subdirectories"
    echo "  -h    Display this help message"
    echo ""
    echo "Examples:"
    echo "  myls  # List the current directory"
    echo "  myls /path/to/directory"
    echo "  myls -l -a /path/to/directory"
    echo "  myls -R /path/to/directory"
}

long_format=false
all_entries=false
dir_name=false
inode_num=false
recursively_list=false

while getopts "ladirR" opt; do
 case $opt in
  l) long_format=true;;
  a) all_entries=true;;
  d) dir_name=true;;
  i) inode_num=true;;
  R) recursively_list=true;;
  h) help; exit 1;;
  ?) echo ":Invaild option: -$opt" >&2; exit 1 ;;
 esac
done

shift $((OPTIND-1))
directory=$1

if [ -z "$directory" ]; then
directory="."
fi

function list {
local options=""

if [ "$long_format" = true ]; then
options+=" -l"
fi

if [ "$all_entries" = true ]; then
options+=" -a"
fi

if [ "$dir_name" = true ]; then
options+=" -d"
fi

if [ "$inode_num" = true ]; then
options+=" -i"
fi

if [ "$recursively_list" = true ]; then
options+=" -R"
fi

ls $options "$directory"
}
list
```

![](/pics/VirtualBoxVM_iBKfoKnRnF.png)

7. **Create a script called `mytest` where:**
   - It check the type of the given argument (file/directory)
   - It check the permissions of the given argument (read/write/execute)

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "Usage: $0 <file or directory>"
    exit 1
fi

file_or_dir=$1
if [ -f "$file_or_dir" ]; then
    echo "$file_or_dir is a regular file."
elif [ -d "$file_or_dir" ]; then
    echo "$file_or_dir is a directory."
else
    echo "$file_or_dir is neither a regular file nor a directory."
fi

echo "Permissions for $file_or_dir:"
echo "Read: $(test -r $file_or_dir && echo "Yes" || echo "No")"
echo "Write: $(test -w $file_or_dir && echo "Yes" || echo "No")"
echo "Execute: $(test -x $file_or_dir && echo "Yes" || echo "No")"
```

![](/pics/VirtualBoxVM_q2eQmUztGj.png)

8. **Create a script called `myinfo` where:**
   - It asks the user about his/her logname.
   - It print full info about files and directories in his/her home directory
   - Copy his/her files and directories as much as you can in /tmp directory.
   - Gets his current processes status.

```bash
#!/bin/bash

read -p "Enter your logname: " user_logname

echo "Full info about files and directories in the home directory:"
ls -l "$HOME"

echo "Copying files and directories to /tmp..."
cp -r "$HOME"/* /tmp

echo "Current process status:"
ps
```

![](/pics/VirtualBoxVM_d6EDqUvQiU.png)
