# Linux Environment and DevOps Assignment

## 1. Linux environment (WSL2)

**Environment:** Ubuntu 22.04.3 LTS running on Windows Subsystem for Linux 2 (WSL2).

From Windows PowerShell, I started the existing Ubuntu environment:

```powershell
wsl -d Ubuntu
```

I ran the following commands **inside Ubuntu**:

```bash
uname -a
whoami
```

**Output:**

```text
Linux Work 5.15.167.4-microsoft-standard-WSL2 #1 SMP Tue Nov 5 00:21:55 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
mikhail2574
```

## 2. Create the project directory tree

**Commands:**

```bash
cd ~
mkdir -p devops-assignment/project/{src,docs,logs}
cd devops-assignment
printf '#!/bin/bash\necho "DevOps application started"\n' > project/src/start.sh
echo "This project demonstrates basic Linux and DevOps skills." > project/docs/README.md
echo "INFO: DEVOPS_TEST application initialized successfully" > project/logs/app.log
find project -print
```

**Output:**

```text
project
project/docs
project/docs/README.md
project/logs
project/logs/app.log
project/src
project/src/start.sh
```

Each of the three required directories contains at least one file.

## 3. Locate a string using find and grep

**Command:**

```bash
find project -type f -exec grep -nH "DEVOPS_TEST" {} +
```

**Output:**

```text
project/logs/app.log:1:INFO: DEVOPS_TEST application initialized successfully
```

`find` selects all regular files under `project`. `grep -nH` searches for `DEVOPS_TEST`, showing the matching filename and line number.

## 4. Set owner-only file permissions

**Commands:**

```bash
chmod 700 project/src/start.sh
ls -l project/src/start.sh
./project/src/start.sh
```

**Output:**

```text
-rwx------ 1 mikhail2574 mikhail2574 46 Nov 10 02:16 project/src/start.sh
DevOps application started
```

**Permission explanation (one sentence):** `-rwx------` means that only the file owner can read, write, and execute the regular file, because `chmod 700` assigns `rwx` to the owner and no permissions to the group or others.

## 5. Software failure and the DevOps lifecycle (reflection, 199 words)

One software failure I read about was the CrowdStrike outage on July 19, 2024. A faulty content configuration update for the Falcon security software caused Windows computers to crash with a blue screen. The impact reached many organizations that depended on those systems, making it a clear example of how a small change can create a large operational failure.

According to CrowdStrike's root cause analysis, the sensor expected 20 input fields while the update supplied 21. This mismatch led to an out-of-bounds memory read. The issue was not a cyberattack; it was a defect that passed through the update validation process.

I believe the **Test** stage of the DevOps lifecycle was the primary opportunity to catch this problem. Automated validation, boundary testing, and integration tests should have covered unexpected input formats before release. The **Release/Deploy** stage was also critical: a canary deployment to a small group of machines, followed by gradual rollout, could have limited the damage. Finally, **Monitor** should detect abnormal crash rates and trigger a rollout stop.

For me, this incident shows that DevOps is not only about deploying faster. It is about making changes safely, observing their effects, and recovering quickly when something goes wrong.

**Source:** [CrowdStrike, Channel File 291 Root Cause Analysis (August 6, 2024)](https://www.crowdstrike.com/en-us/blog/channel-file-291-rca-available/)

## What DevOps means to me

DevOps is a way of organizing software development and operations around shared responsibility for the complete lifecycle of a service. It combines automation, continuous testing, controlled deployments, monitoring, and feedback so that teams can ship changes frequently without sacrificing reliability.

## Terminal screenshot

See the accompanying `terminal-screenshot.png`, captured from my Ubuntu WSL2 terminal showing the environment, commands, permissions, and script execution.
