# File Permissions in Linux

## Check file and directory details

![image](https://github.com/jhung-cybersecurity/Linux-Commands_File-Permissions/assets/139807613/6d8a80aa-c547-47d3-9f54-c07831c8567a)

**Steps I performed for the result above:**  

1. In order to check the files and directory details, I begin by checking our current location using `pwd`.
2. I navigate to `cd ~/projects` where the files are.
3. I use the command `ls -la` to display the contents and permissions of the `projects` directory, including the hidden files which in this case is, `.project_x.txt`.



## Describe the permissions string

Using the screenshot above that I performed as reference and looking at `drafts` for example. The permission string reads `drwx--x---`.  

To break it down:  

1. The first letter will either be a `d` or `-`, which indicates that it is either a directory or a file respectively. In this particular example, this is a directory as indicated by a `d`.
2. The 2nd to the 4th letter indicates permissions for the `user` group.  
   * The `r` indicates that the `user` has read permissions  
   * The `w` indicates that the `user` has write permissions  
   * The `x` indicates that the `user` has execute permissions  
3. The 5th to the 7th letter indicates permissions for the `group` group.
   * Since the 5th and 6th location is a hyphen, that indicates there's no read or write permissions
   * The `x` indicates that the `group` group has execute permissions
5. The 8th to the 10th letter indicates permissions for the `other` group.
   * Since the permission string are all hyphens for the 8th to the 10th letter location, that indicates there's no read, write, or execute permissions for the `other` group.  


## Change file permissions

![image](https://github.com/jhung-cybersecurity/Linux-Commands_File-Permissions/assets/139807613/7abb82b5-2f5a-49f5-b802-6f3a0c79d3e0)

**Steps I performed for the result above:**  

1. The organization doesn't want the `other` users to write to any files. After reading through the permission strings, I find that `project_k.txt` has write permissions for the `other` users.
2. I use `chmod o-w project_k.txt` command to remove the write permission for the `other` users.
3. I check that the command above is correct by using `ls -l`. I omit `ls -la` because `project_k.txt` is not a hidden file.
4. Next, the organization states that `project_m.txt` is a restricted file and should not be readable or writeable by the `group` or `other`, only the `user` should have these permissions.
5. After finding that `project_m.txt` has read permissions, I went ahead and removed that by using `chmod g-r project_m.txt`.
6. I check my work using `ls -l` once more.
7. `project_m.txt` is now only readable and writeable by the `user`. 


## Change file permissions on a hidden file

![image](https://github.com/jhung-cybersecurity/Linux-Commands_File-Permissions/assets/139807613/4e2da519-8a4d-4f13-9d1a-084949b019cb)

**Steps I performed for the result above:**  

1. The hidden file `.project_x.txt` has been archived and should not be written to by anyone. However, the `user` and `group` should still be able to read this file. 
2. I use `ls -la` to display the hidden file and review its permissions.
3. Since the string is indicating that the `user` and `group` both has write permissions, I went ahead and changed that by using `chmod u-w,g-w .project_x.txt`.
4. I use `ls -la` to check my work.
5. Now that `group` is missing read permission so I use `chmod g+r .project_x.txt.
6. I use `ls -la` to check my work. 

```
I am aware that using `chmod u=r,g=r .project_x.txt` would simply rewrite the permissions using fewer steps.
However, by taking extra steps, I am able to showcase my full understanding of the command strings.
```


## Change directory permissions

![image](https://github.com/jhung-cybersecurity/Linux-Commands_File-Permissions/assets/139807613/929b2980-4fdd-4ef9-b50a-ea4a068761bf)

**Steps I performed for the result above:**  

1. I need to check the permissions of the `drafts` subdirectory. To do that, I use `ls -l`.
2. I see that the `group` have permissions set to access the drafts directory and its contents.
3. To fix that, I use `chmod g-x drafts`.
4. I check my work using `ls -l`.

## Summary

Throughout this Linux showcase, I am constantly checking my current path using `pwd` and my work using `ls -l` or `ls -la` to display hidden files. The permission strings are indicated by 10 letters, of which are `drwxrwxrwx` and is replaced by `-` if there's no permissions. In the case of the first letter, the `-` indicates a file instead of a directory. In order to add or remove permissions, `chmod` is used. More specifically, `chmod u-r,g-r,o-r project.txt` indicates that `user`, `group` and `other` will have read permissions removed. This can also be achieved by the `=` command which will look like `chmod u=r project.txt`. However, this will rewrite the permission.  

Changing permission is an important and necessary knowledge in the field of cybersecurity and I hope that I am able to showcase my understanding of this subject.
