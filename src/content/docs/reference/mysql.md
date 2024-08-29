---
tags:
- MySQL
- database
title: MySQL Database Import
type: docs

series: 
- docs 
- Wordpress
---

### For quick large MySQL database import use:

Manual mode by copy paste in terminal.

```  {filename="Start of file"}
sed -i '1s/^/SET autocommit = 0;\n/' dump.sql


```

```  {filename="End of file"}
echo 'COMMIT;' >> dump.sql


```
### Or create bash script to run the above commands.
```  {filename="#!/bin/bash"}
#!/bin/bash

# Check if filename is provided as argument
if [ $# -eq 0 ]; then
    echo "Usage: $0 <filename>"
    exit 1
fi

filename=$1

# Add 'SET autocommit = 0;' at the beginning of the file
sed -i '1s/^/SET autocommit = 0;\n/' "$filename"

# Append 'echo 'COMMIT;' to the end of the file
echo 'COMMIT;' >> "$filename"

echo "Now import it. quickly :)"

```