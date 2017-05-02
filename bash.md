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
find . ! -name 'toKeep.txt' -type f -exec rm -f {} +
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
tring="1;2"
echo $string | cut -d';' -f1 # output is 1
echo $string | cut -d';' -f2 # output is 2
```

```
echo "abc : def" | awk -F' : ' '{print $1}'
```


### Split string into an array by delimeter

```
IN="bla@some.com;john@home.com"
arrIN=(${IN//;/ })
echo ${arrIN[0]}
echo ${arrIN[1]}
```


### Free space available in current directory

```
df -Ph . | tail -1 | awk '{print $4}'
```


### Sizes of directories

```
du -sh ./*
```


### Numeric equality

```
if (( var == 3 )); then
    echo "yes"
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
if [ -e "$FILE" ]; then
    # Will enter here if $FILE exists, even if it contains spaces
fi
```


### Logical operators

```
if (! (( var == 2 || var < 30 ))) && [[ ${str} == abc ]]; then
    # do something
fi
```

If (not ((var == 2) or (var < 30)) and (str is abc))


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


### Remove the first 5 characters from each filename

```
rename -n 's/(.{5})(.*)$/$2/' *.*
```
The `-n` is for simulating; remove it to get the actual result.


### Remove last 4 characters from a string

```
v="some string.rtf"
v2=${v::-4}
echo "$v --> $v2"
```


### Copy every fourth file in a folder

```
cp $(printf '%s\n' im???.jpg | awk 'NR%4 == 1') /some/place
```


### Renaming files in a folder to sequential numbers

```
a=1
for i in *.png; do
	new=$(printf "%03d.png" "$a")
	mv -- "$i" "$new"
	let a=a+1
done
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
: <<'END'
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
poseFiles=(/path/*.pkl)
```


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


### Rotate images in a folder

```
for file in ./*.png; do
    convert "$file" -rotate 90 "${file%.png}"_rotated.png
done
```
