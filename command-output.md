# Linux Command Record

Commands were run in a Linux x86_64 environment. Outputs below are copied from
the terminal session.

## 1. Environment

```console
$ uname -a
Linux localhost 6.18.35 #1 SMP Mon Aug 31 18:10:37 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

$ whoami
root
```

## 2. Create and populate the directory tree

```console
$ mkdir -p project/{src,docs,logs}
$ printf '#!/usr/bin/env bash\nset -euo pipefail\n\necho "Service health: OK"\n' > project/src/health_check.sh
$ printf '%s\n' '# DevOps Reflection' > project/docs/devops-response.md
$ printf '%s\n' '2026-09-02T18:24:01Z ERROR service=video-gateway event=CONNECTION_FAILED source=camera-01' > project/logs/application.log
$ find project -type f | sort
project/docs/devops-response.md
project/logs/application.log
project/src/health_check.sh
```

The files were subsequently completed with the content committed in this
repository.

## 3. Locate files and search for a string

The selected string was `CONNECTION_FAILED`.

```console
$ find project -type f -name "*.log"
project/logs/application.log

$ grep -Rni --exclude-dir=.git "CONNECTION_FAILED" project
project/logs/application.log:2:2026-09-02T18:24:01Z ERROR service=video-gateway event=CONNECTION_FAILED source=camera-01
```

`find` locates log files by filename, while `grep` recursively locates the
specified text and reports its filename and line number.

## 4. Owner-only executable permission

```console
$ chmod 700 project/src/health_check.sh
$ ls -l project/src/health_check.sh
-rwx------ 1 root root 66 Sep  2 22:43 project/src/health_check.sh

$ ./project/src/health_check.sh
Service health: OK
```

The permission string is `-rwx------` because the owner has read, write, and
execute permissions, while the group and all other users have no permissions.

## 5. Written response

The 150–250 word response is available in
[`project/docs/devops-response.md`](project/docs/devops-response.md).
