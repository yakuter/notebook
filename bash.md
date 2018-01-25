# bash

My personal notes about bash

#### Change file names in a directory

Example: 
05_h.png
06_h.png

to

05_half.png
06_half.png

```bash
for file in *_h.png
do
  mv "$file" "${file/_h.png/_half.png}"
done
```

### Conditions

#### Check if a variable is empty:

```bash
if [[ -z "${foobar// }" ]]; then
fi
```

#### Check if a variable is not empty:

```bash
[[ -n "${foobar// }" ]]
```

#### Check if a file exists:

```bash
if [ -f $FILE ];
then
   echo "File $FILE exists."
else
   echo "File $FILE does not exist."
fi
```

#### Check if a string contains another string

```bash
string='My long string'
if [[ $string == *"My long"* ]]; then
  echo "It's there!"
fi
```

#### Check if a command exists

Definition:
```bash
  command_exists () {
      type "$1" &> /dev/null ;
  }
```

Usage:

```
  if command_exists foo ; then
      echo "yo"
  fi
```

### loops

#### Iterate Files

```bash
for i in *; do echo $i; done
```

#### Rename bunch of files

```bash
for name in *
do
    newname=new-"$(echo "$name" | cut -c7-)" # cuts first 6 characters
    mv "$name" "$newname"
done
```

#### iterating input by line and columns

```bash
lsblk | awk '{print $1,$4}' > input.txt

while read col1 col2 ; do
  echo "$col1 $col2"
done < input.txt
```

### dialogs

#### opening a menu with bunch of lines

```bash
regionsArray=()

while read i name; do
  regionsArray+=($i "$name")
done <<< "$regions"

selected=$(dialog --stdout \
                  --title "Timezones" \
                  --backtitle "Happy Hacking Linux" \
                  --ok-label "Next" \
                  --no-cancel \
                  --menu "Select a continent or ocean from the menu:" \
                  20 50 30 \
                  "${regionsArray[@]}")
```


