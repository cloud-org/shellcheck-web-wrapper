<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [shellcheck-web-wrapper](#shellcheck-web-wrapper)
  - [dev](#dev)
  - [acknowledgement](#acknowledgement)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## shellcheck-web-wrapper

为 shellcheck 提供一个 web 接口

### dev

```go
go build 
./shellcheck-web-wrapper
```

HTTP 服务将暴露 7777 端口

```sh
# ashing @ ashing-virtual-machine in ~ [17:22:35] 
$ curl --location --request POST 'http://127.0.0.1:7777/v1/shellcheck' \
--header 'Content-Type: application/json' \
--data-raw '{
    "script": "#!/bin/bash\nrm -rf /\necho ${hello}"
}' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   468  100   412  100    56  65025   8838 --:--:-- --:--:-- --:--:-- 68666
{
  "comments": [
    {
      "line": 2,
      "endLine": 2,
      "column": 8,
      "endColumn": 9,
      "level": "warning",
      "code": 2114,
      "message": "Warning: deletes a system directory."
    },
    {
      "line": 3,
      "endLine": 3,
      "column": 6,
      "endColumn": 14,
      "level": "warning",
      "code": 2154,
      "message": "hello is referenced but not assigned."
    },
    {
      "line": 3,
      "endLine": 3,
      "column": 6,
      "endColumn": 14,
      "level": "info",
      "code": 2086,
      "message": "Double quote to prevent globbing and word splitting."
    }
  ]
}

```

### acknowledgement

- echo web framework
- shellcheck
