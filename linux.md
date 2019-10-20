### Shebang

```
#!/usr/bin/env bash
```


### Find all files containing specific text

```
grep -rnw '/path/to/somewhere/' -e "pattern"
```


### Find file in current directory

```
find . -name "libstdc++*"
```


### Find string in a directory

```
grep -R 'string' dir/
```


### Remove all files but one

```
find . ! -name 'to-keep.txt' -type f -maxdepth 1 -exec rm -f {} +
```


### Relative path to absolute

```
readlink -m /x/y/../../a/b/z/../c/d
```

gives

```
/a/b/c/d
```


### Get current user

```
whoami
```


### Parse filename/path/extension

```
a=/tmp/xx/file.tar.gz
xpath=${a%/*}
xbase=${a##*/}
xfext=${xbase##*.}
xpref=${xbase%.*}
echo ${a}
echo path=${xpath}
echo pref=${xpref}
echo ext=${xfext}
```


### Parse string by a single-character delimiter

```
string="1;2"
echo $string | cut -d';' -f1 # output is 1
echo $string | cut -d';' -f2 # output is 2
```

```
echo "abc : def" | awk -F' : ' '{print $1}'
```


### Split string into an array by delimeter

```
str="bla@some.com;john@home.com"
arr=(${str//;/ })
echo ${arr[0]}
echo ${arr[1]}
```


### String starts with

```
# The == comparison operator behaves differently within a double-brackets
# test than within single brackets.

[[ $a == z* ]]   # True if $a starts with a "z" (wildcard matching).
[[ $a == "z*" ]] # True if $a is equal to z* (literal matching).
```


### Free space available in current directory

```
df -Ph . | tail -1 | awk '{print $4}'
```


### Sizes of directories

```
du -sh ./*
```


### Or, and, not in if

```
a=true
b=false

if ${a} || ${b}; then
    echo true
fi

if ${a} && ! ${b}; then
    echo true
fi
```


### Numeric equality

```
if (( var == 3 )); then
    echo "yes"
fi
```


### Mod

```
$((i%n_per_session))
```


### Float comparison

```
num1=10
num2=0.1
if (( $(echo "$num1 > $num2" | bc -l) )); then
    :
fi
```


### String equality

```
if [[ ${str} == 3 ]]; then
    echo "yes"
fi
```


### Check if directory exists

```
if [ -d "$DIRECTORY" ]; then
    # Will enter here if $DIRECTORY exists, even if it contains spaces
fi
```


### Check if file exists

```
if [[ -e "$FILE" ]]; then
    # Will enter here if $FILE exists, even if it contains spaces
fi
```


### Logical operators

```
if (! (( var == 2 || var < 30 ))) && [[ ${str} == abc ]]; then
    # do something
fi
```


### Loop through only directories

```
for f in *; do
    if [[ -d $f ]]; then
        # $f is a directory
    fi
done
```


### Else

```
if [ "$seconds" -eq 0 ]; then
   timezone_string="Z"
elif [ "$seconds" -gt 0 ]; then
   timezone_string=$(printf "%02d:%02d" $((seconds/3600)) $(((seconds / 60) % 60)))
else
   echo "Unkown parameter"
fi
```


### Until string is empty

```
pid=$(...)
until [ -z "$pid" ]; do
    kill -9 "$pid"
    pid=$(...)
done
```


### Loop through elements in array

```
clips=( "ballet11-2" "jogging" )
for clip in "${clips[@]}"; do
	frameDir=/data/clips/${clip}
done
```


### Loop through elements with index

```
arr=( 7 12 16 )
for i in "${!arr[@]}"; do # for (( i = 0; i < ${#arr[@]}; i++ )); do
    printf "%s\t%s\n" "$i" "${arr[$i]}"
done
```


### Batch rename

```
#!/usr/bin/env bash

for cat_dir in ./jobs/*; do
    for obj_file in $cat_dir/*.m; do
        xpath=${obj_file%/*}
        xbase=${obj_file##*/}
        echo "$obj_file -> $xpath/prefix_$xbase"
    done
done
```


### Remove the first 5 characters from each filename

```
rename -n 's/(.{5})(.*)$/$2/' *
```
The `-n` is for simulating; remove it to get the actual result.


### Remove last 4 characters from a string

```
v="some string.rtf"
v2=${v::-4}
echo "$v --> $v2"
```


### Remove fixed prefix/suffix from a string

```
foo=${string#$prefix}
foo=${string%$suffix}
```
There are also `##` and `%%`, which remove as much as possible if `$prefix` or `$suffix` contains wildcards.


### Copy every fourth file in a folder

```
cp $(printf '%s\n' im???.jpg | awk 'NR%4 == 1') /some/place
```


### Rename files in a folder to sequential numbers

```
a=1; for i in *.png; do new=$(printf "%03d.png" "$a"); mv -- "$i" "$new"; let a=a+1; done
```


### Check if element in array


```
array_contains2 () { 
    local array="$1[@]"
    local seeking=$2
    local in=1
    for element in "${!array}"; do
        if [[ $element == $seeking ]]; then
            in=0
            break
        fi
    done
    return $in
}
array_contains2 arr "a b"  && echo yes || echo no    # no
array_contains2 arr "d e"  && echo yes || echo no    # yes
```


### Array length, indices, contents

```
a=(1 1 2 3 4)
echo ${a[@]}
echo ${!a[@]}
echo ${#a[@]}
```


### Append to array

```
ARRAY=()
ARRAY+=('foo')
ARRAY+=('bar')
echo ${ARRAY[0]}
```


### Assign command output to variable

```
n=$(ls *.py | wc -l)
```


### Extract the n-th line of file

```
sed '68q;d' param1.csv
```


### Block comment

```
#!/bin/bash
echo before comment
: <<-'END'
bla bla
blurfl
END
echo after comment
```


### Kill all jobs by me

```
pkill -9 -u `id -u xiuming`
```


### Pretty print `$PATH`

```
tr ':' '\n' <<< "$PATH"
```


### Download repo from GitHub

```
git clone git://github.com/vim/vim.git
```


### Locate a binary

```
type -a python
```


### Download a file from web

```
wget http://website.com/files/file.zip
```


### Determine contents of binary files

```
strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
```


### Arithmetic operations

```
idx=$((idx+1))
```


### Wildcard exluding a pattern

```
find /path/ -name 'foo*.png' -a ! -name 'bar*.png'
```

Filenames are NOT ordered.


### Collect filenames into an array

```
files=(/path/*.pkl)
```


### Find latest file in directory

```
ls -t *.png | head -1
```

Sort by time with `-t`. Grab the first (newest) with `head -1`.


### Release a port

```
lsof -i :<port>
kill -9 <PID>
```


### Extract a column

```
30-103-178:~ x$ lsof -i :5901
COMMAND  PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ssh     3751    x    6u  IPv6 0x92a5ebb41be479d3      0t0  TCP localhost:5901 (LISTEN)
ssh     3751    x    7u  IPv4 0x92a5ebb42075b35b      0t0  TCP localhost:5901 (LISTEN)
30-103-178:~ x$ lsof -i :5901 | tail -n1 | awk '{print $2;}'
3751
```


### Single quotes inside single quotes

```
alias rxvt='urxvt -fg '"'"'#111111'"'"' -bg '"'"'#111111'"'"
#                     ^^^^^       ^^^^^     ^^^^^       ^^^^
#                     12345       12345     12345       1234
```

3 `'` is the quoted character.


### Redirect (or slicence) `stdout` and `stderr`

```
# Send stdout to out.log, stderr to err.log
myprogram > out.log 2> err.log

# Send both stdout and stderr to out.log
myprogram &> out.log      # New bash syntax
myprogram > out.log 2>&1  # Older sh syntax

# Log output, hide errors.
myprogram > out.log 2> /dev/null

# Hide both
myprogram &> /dev/null
```


### Get image dimensions

```
wxh=$(identify "$im_f" | cut -d' ' -f3)
w=$(echo "$wxh" | awk -F'x' '{print $1}')
h=$(echo "$wxh" | awk -F'x' '{print $2}')
```


### SSH timeout

```
ssh -o ConnectTimeout=10 -o BatchMode=yes -o StrictHostKeyChecking=no -q ${user}@vision${ID}.csail.mit.edu "exit"
```

`-o ConnectTimeout=10` sets timeout to be 10 seconds, `-o BatchMode=yes` keeps SSH from hanging with an unknown host and adds it to `known_host`, and `-o StrictHostKeyChecking=no` adds the fingerprint automatically (be careful!).


### Case

```
case ${clip} in
    "ballet1")
        eval "${cmd1}"
        ;;
    *)
        eval "${cmd2}"
        ;;
esac
```


### Fast way of removing large/deep folder

```
mkdir empty_dir; rsync -a --delete empty_dir/ your_dir/; rm -rf  empty_dir/
```


### Shuffle array

```
arr=( 1 2 3 4 )
arr_shuffled=( $(echo "${arr[@]}" | sed -r 's/(.[^;]*;)/ \1 /g' | tr " " "\n" | shuf | tr -d " " ) )
echo "${arr_shuffled[@]}"
2 4 3 1
```


### `rsync`

```
rsync -avzhP --dry-run xiuming@visiongpu20.csail.mit.edu:/data/vision/billf/webCNN/xiuming ~/Desktop/output
```

`-v`: verbose

`-r`: copies data recursively (but don’t preserve timestamps and permission while transferring data)

`-a`: archive mode, archive mode allows copying files recursively and it also preserves symbolic links, file permissions, user & group ownerships and timestamps

`-z`: compress file data

`-h`: human-readable, output numbers in a human-readable format

`-P`: show progress

`--remove-source-files`


### Zip

```
zip -j myzip file1 file2 file3
```
stores just the name of a saved file (junks the path), and does not store directory names.

```
zip -r myzip directory/
```
recursively zips the files, maintaining the file structure.


### Unzip

```
tar -xvzf images.tar.gz
```

`f`: this must be the last flag of the command, and the tar file must be immediately after. It tells tar the name and path of the compressed file

`z`: tells tar to decompress the archive using g**z**ip

`x`: tar can collect files or e**x**tract them. `x` does the latter

`v`: verbose

```
tar -xvf yourfile.tar
```


### Move all but one file

```
mv !(fileOne) ~/path/newFolder
```

with `shopt -s extglob` in `.bashrc`


### Sort results by `find` and print filename only

```
find ./ -maxdepth 1 -name '*.pkl' -printf "%f\n" | sort | head -1
```


### Show current libraries

```
ldconfig -p | grep libx264.so
```


### Replace character in string with another character

```
foo="1 2 3"
bar=${foo/ /-}
```

replaces first blank only.

```
bar=${foo// /-}
```

replaces all blanks.


### Slice array

```
$ foo=(q w e r t y u)
$ echo "${foo[@]:0:4}"
q w e r
```


### Dictionary

```
declare -A dict=( [key1]="1,2,3 a,b,c" [key2]="1 x" )

key=key1
echo ${dict[${key}]}
```


### Read space-delimited strings into array

```
read -r -a arr <<< "first,string second,string"

echo ${arr[0]}
echo ${arr[1]}
```


### Read lines of file into array

```
readarray a < /path/to/filename
```


### First N characters of a string variable

```
a=g16
echo ${a:0:1}
echo ${a:0:2}
```


### Unpack elements from string

```
arr=( 1 2 3 4 )
read -r e1 e2 e3 _ <<< "${arr}"

echo ${e1}
echo ${e2}
echo ${e3}
```


### Parse elements by delimiter

```
strarr=1,2,3,4
IFS=, read -r e1 e2 e3 _ <<< "${strarr}"
```


### Loop through lines in file

```
while read c; do
    ssh -n "$me@$host" "$c; exit" &
done <cmd_list.txt
```

By default, `ssh` reads from `stdin`, which is your input file. As a result, you only see the first line processed, because `ssh` consumes the rest of the file, and your `while` loop terminates. To prevent this, pass the `-n` option to your `ssh` command to make it read from `/dev/null` instead of `stdin`.

When in conflict with breaking from another while loop, use the following instead.

```
for line in `cat "${filepath}"`; do
    echo $line
done
```


### Reveal .so library

```
ldd ${CAFFE_DIR}/bin/caffe | grep boost
```

```
ldd ${MOON_DIR}/software/blender_build/bpy.so | grep libpng
```


### Get over "device or resource busy"

```
lsof +D <path>
kill -9 <PID>
```


### Print formatted string to variable

```
printf -v my_str "%03d" "${my_int}"
```

Useful for prepending zeros to integers.


### Check if string is valid as an integer

```
[[ $var =~ ^-?[0-9]+$ ]]
```


### Loop through files in reverse order

```
files=(/var/logs/foo*.log)
for ((i=${#files[@]}-1; i>=0; i--)); do
    bar "${files[$i]}"
done
```


### Show image info

```
file /path/to/img.png
```


### Unique elements of array

```
sorted_unique_ids=($(echo "${ids[@]}" | tr ' ' '\n' | sort -u | tr '\n' ' '))
```


### Substring

```
string='My long string'
if [[ $string == *"My long"* ]]; then
  echo "It's there!"
fi
```


### `ls` with error handling

```
if ls "${out_dir}"/*.blend 1> /dev/null 2>&1; then
    first_file=$(ls "${out_dir}"/*.blend | head -1)
else
    first_file=none
fi
```


### Number range in regex

```
cp 0[2-9]?.npz ./
```
copies `020.npz`, `021.npz`, ..., `030.npz`, ..., `099.npz`.


### Generate a number sequence

```
me@host:~$ vals=($(seq 0 1 10))
me@host:~$ echo "${vals[@]}"
0 1 2 3 4 5 6 7 8 9 10

me@host:~$ arr=(./*.png)
me@host:~$ echo ${#arr[@]}
10
me@host:~$ ind=($(seq 0 1 $((${#arr[@]}-1))))
me@host:~$ echo "${vals[@]}"
0 1 2 3 4 5 6 7 8 9
```


### Check `sudo` commands on machine

```
sudo cat /var/log/auth.log | grep sudo
```


### Replace string in file
```
sed -i -e 's/abc/XYZ/g' /tmp/file.txt
```
replaces `abc` with `XYZ` in file `/tmp/file.txt`.


### Return Python list to bash

```
result_arr=($(python script.py param1 param2 | tr -d '[],'))
echo "${result_arr[@]}"
```


### Strip single quotes for each element of an array

```
abc=(${abc[@]//\'/})
```


### Call functions defined in `.bashrc`

Do any of the following.

* Source `.bashrc` explicitly:
    ```
    #!/bin/bash
    . ~/.bashrc
    exr2npz "foo" "bar"
    ```

* Start bash with the interactive flag:
    ```
    #!/bin/bash -i
    exr2npz "foo" "bar"
    ```

* Set `BASH_ENV` when you start your script:
    ```
    BASH_ENV=$HOME/.bashrc /path/to/my/script
    ```


### When the username gets truncated by `+` in `top`

Use the "long-username version" of `ps -aux`

```
ps axo user:20,pid,pcpu,pmem,vsz,rss,tty,stat,start,time,comm
```


### Send a command to run in background on a remote machine

```
ssh -n -f user@host "sh -c 'cd /whereever; nohup ./whatever > /dev/null 2>&1 &'"
```
