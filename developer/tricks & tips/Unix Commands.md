### UNIX CLIs

```bash
# Counting the number of files
ls -l /path/to/directory | grep -c ^-

# Open image
eog [filename]

# Register any path to home
ln -sf [path] [name]
~/[name]

# Decrease or increase font size of terminal window
ctl + [-] | ctl + [+]

# Kill the running process
lsof -i tcp:3000    // http or https
kill -9 197058      // 197058 - [process ID]

# zip packages for AWS lambda function
pip3 install [pkg_name] -t
zip -r [func_name].zip

# replace filename with pattern in multiple files
for f in NONAME-*; do mv $f "`echo $f | sed 's/NONAME-//'`"; done
```

To get the available storage space on your Ubuntu system, you can use the **`df`** command (short for "disk free"). Here's an example command that will display the available space on all mounted filesystems:

```jsx
df - h;
```

To get the total count of items (files and directories) in the current directory and all its subdirectories in Ubuntu, you can use the **`find`** command along with the **`wc`** command. Here's an example command that will display the total count of items:

```jsx
find . -type f -o -type d | wc -l
```

To get the size of a folder in Ubuntu, you can use the **`du`** command (short for "disk usage"). Here's an example command that will display the size of the folder **`/path/to/folder`**:

```jsx
du - sh / path / to / folder;
```
