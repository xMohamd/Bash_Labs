**Using sed utility**

1. **Display the lines that contain the word “lp” in /etc/passwd file.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.005.png)

2. **Display /etc/passwd file except the third line.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.006.png)

3. **Display /etc/passwd file except the last line.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.007.png)

4. **Display /etc/passwd file except the lines that contain the word “lp”.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.008.png)

5. **Substitute all the words that contain “lp” with “mylp” in /etc/passwd file.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.009.png)

**Using awk utility**

1. **Print full name (comment) of all users in the system.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.010.png)

2. **Print login, full name (comment) and home directory of all users (Print each line preceded by a line number).**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.011.png)

3. **Print login, uid and full name (comment) of those uid is greater than 500**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.012.png)

4. **Print login, uid and full name (comment) of those uid is exactly 500**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.013.png)

➔ If uid = 999 instead of 500

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.014.png)

5. **Print line from 5 to 15 from /etc/passwd**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.015.png)

6. **Change lp to mylp**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.016.png)

7. **Print all information about greatest uid.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.017.png)

8. **Get the sum of all accounts id’s.**

![](/pics/Aspose.Words.2d90fae2-6dff-4688-a4d7-b8fa8439c37c.018.png)

**Bonus:**

1. **Get the sum of accounts id’s that has the same group.**

```bash
awk -F: '{sum[$4]+=$3} END { for (gid in sum) print "Group " gid ": " sum[gid]}' /etc/passwd
```

2. **Make the following report:**

```txt
User-Group Report
--------------------------
Group1 Name:
User1
User2
Group2 Name:
User3
User4
```

```bash
awk -F: '{user[$4]=user[$4] $1 " "} END { for (gid in user) {print "Group" gid " Name: "; print user[gid] }}' /etc/passwd
```
