### Dependencies:
* [astyle](http://astyle.sourceforge.net/)

# Add the following pre-commit hook:
```
#!/bin/bash
    
cd "$(git rev-parse --show-toplevel)"
    
ASTYLE=astyle
if git rev-parse --verify HEAD >/dev/null 2>&1
then
       against=HEAD
fi

ASTYLE_PARAMETERS="--options=../build/style.options "

echo "--Formatting source code--"

files=\`git-diff-index --diff-filter=ACMR --name-only -r --cached $against --\`
for file in $files; do
    x=`echo $file |grep -E '(\.java)' |grep -v scripts`
    if test "x$x" != "x"; then
        $ASTYLE ${ASTYLE_PARAMETERS} $file
        git add $file
    fi
done
```