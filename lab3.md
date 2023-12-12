1. **Write a script called `mycase`, using the case utility to checks the type of character entered by a user:**
   - Upper Case.
   - Lower Case.
   - Number.
   - Nothing.

```bash
#!/bin/bash

read -p "Enter a character: " ch

case $ch in
  [A-Z]) echo "Upper case" ;;
  [a-z]) echo "Lower case" ;;
  [0-9]) echo "Number" ;;
  "") echo "Nothing entered" ;;
  *) echo "Unknown character" ;;
esac
```

![](/pics/VirtualBoxVM_T9KprpfaC4.png)

2. **Enhanced the previous script, by checking the type of string entered by a user:**

- Upper Cases.
- Lower Cases.
- Numbers.
- Mix.
- Nothing.

```bash
#!/bin/bash

read -p "Enter a string: " str
shopt -s extglob
case "$str" in
  +([A-Z]) ) echo "Upper cases" ;;
  +([a-z]) ) echo "Lower cases" ;;
  +([0-9]) ) echo "Numbers" ;;
  +([0-9|a-zA-Z]) ) echo "Mix" ;;
  "" ) echo "Nothing entered" ;;
  * ) echo "Unrecognized string" ;;
esac
```

![](/pics/VirtualBoxVM_9xS8Q5gM04.png)

3. **Write a script called `mychmod` using for utility to give execute permission to all files and directories in your home directory.**

```bash
#!/bin/bash

for file in $HOME/*
do
    chmod +x "$file"
done
```

4. **Write a script called `mybackup` using for utility to create a backup of only files in your home directory.**

```bash
#!/bin/bash

backup_dir="$HOME/backup"
backup_file="$backup_dir/backup.tar.gz"

if [ ! -d "$backup_dir" ]; then
    mkdir "$backup_dir"
fi

files=()
for file in "$HOME"/*; do
    if [[ -f "$file" ]]; then
        files+=("$file")
    fi
done


tar czf "$backup_file" -C "$HOME" "${files[@]}" 2>/dev/null

echo "Backup created successfully: $backup_file"
```

![](/pics/VirtualBoxVM_NTv4F9iViF.png)

5.  **Write a script called `mymail` using for utility to send a mail to all users in the system.**

- Note: write the mail body in a file called `mtemplate`.

```bash
#!/bin/bash

mail_template="mtemplate"

for user in $(cut -f1 -d: /etc/passwd)
do
    mail -s "Subject" "$user" < "$mail_template"
done
```

6. **Write a script called `chkmail` to check for new mails every 10 seconds.**
   - Note: mails are saved in /var/mail/username

```bash
#!/bin/bash

while true; do
    new_mails=$(mail -n /var/mail/username | wc -l)
    if [[ $new_mails -gt 0 ]]; then
        echo "You have $new_mails new mails!"
        mail -n /var/mail/username
    fi
    sleep 10
done
```

Bonus: Open a talk session to a certain user when she/he logs into the system.
**We will need to add next 2 lines in .bashrc**

```bash
# Display a welcome message
echo "Welcome to the system, $(whoami)!"
# Start a chat session to a specific user
write <username> #replace <username> with your actually username
```

![](/pics/VirtualBoxVM_8Wfh84zBUW.png)

7. **What is the output of the following script**

```bash
typeset –i n1
typeset –i n2
n1=1
n2=1
while test $n1 –eq $n2
do
n2=$n2+1
print $n1
if [ $n1 –gt $n2 ]
then
break
else
continue
fi
n1=$n1+1
print $n2
done
```

![](/pics/VirtualBoxVM_xMvNzAsH1J.png)

8. **Create the following menu (Using select utility then while utility):**

- Press 1 to ls
- Press 2 to ls –a
- Press 3 to exit

```bash
#!/bin/bash

select choice in "ls" "ls -a" "Exit"; do
        case $choice in
            "ls")
                ls
                break
                ;;
            "ls -a")
                ls -a
                break
                ;;
            "Exit")
                exit 0
                ;;
            *)
                echo "Invalid choice."
                ;;
        esac
done
```

![](/pics/VirtualBoxVM_NQqWpHdJrU.png)

9. **Write a script called `myarr` that ask a user how many elements he wants to enter in an array, fill the array and then print it.**

```bash
#!/bin/bash

echo "Enter the number of elements in the array: "
read num_elements

declare -a my_array

for ((i=0; i<$num_elements; i++))
do
    read my_array[i]
done

echo "Array elements: ${my_array[@]}"
```

![](/pics/VirtualBoxVM_iSeHedB8tC.png)

10. **Write a script called `myavg` that calculate average of all numbers entered by a user.**

- Note: use arrays

```bash
#!/bin/bash

declare -a numbers
sum=0
count=0

while true; do
  read -p "Enter a number (or q to quit): " num
  if [[ $num == "q" ]]; then
    break
  fi

  if [[ $num =~ ^[0-9]+$ ]]; then
    numbers[count++]=$num
    sum=$((sum + num))
  else
    echo "Invalid input. Please enter a number."
  fi
done

if [[ $count -gt 0 ]]; then
  avg=$((sum / count))
  echo "Average: $avg"
else
  echo "No valid numbers entered."
fi
```

![](/pics/VirtualBoxVM_uW83uLqjEB.png)

11. **Write a function called `mysq` that calculate square if its argument.**

```bash
#!/bin/bash

function mysq {
    if [ -z "$1" ]; then
        read -p "Enter a number: " number
    else
        number="$1"
    fi

    if ! [[ "$number" =~ ^[0-9]+$ ]]; then
        echo "Error: '$number' is not a valid number."
        return 1
    fi

    local square=$((number * number))

    echo "The square of $number is $square"
}
mysq
```

![](/pics/VirtualBoxVM_CNhaTHzXUR.png)
