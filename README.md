# Linux and DevOps Basics

This repository demonstrates a working Linux environment, basic command-line
operations, Unix file permissions, and an understanding of the DevOps lifecycle.

## Repository contents

```text
.
├── README.md
├── command-output.md
├── terminal-screenshot.png
└── project
    ├── docs
    │   └── devops-response.md
    ├── logs
    │   └── application.log
    └── src
        └── health_check.sh
```

## Run the example

```bash
./project/src/health_check.sh
```

## Verify the search tasks

```bash
find project -type f -name "*.log"
grep -Rni --exclude-dir=.git "CONNECTION_FAILED" project
```

The complete commands and captured output are recorded in
[`command-output.md`](command-output.md). The written DevOps response is in
[`project/docs/devops-response.md`](project/docs/devops-response.md).

