---
title: guten tag
---

## toc

- [blog](blog)

## some code

```bash
#!/bin/bash

app=$(basename "$0")

function usage { cat << EOF
usage: $app input output
EOF
}

[[ $# -eq 2 ]] || {
  usage >&2
  exit 1
}
```
