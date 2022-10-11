# Azure CLI ARM64 install bug repro

MacOS 12.3.1 (M1 Max)
VSCode 1.72.0
Remote Containers v0.259.0
Docker Desktop 4.12.0 (85629)
Docker Engine 20.10.17

Steps:

1. Open this repository in VSCode and Rebuild and Reopen in Container
2. The build will fail with output similar to what's below. Edit the `devcontainer.json` locally, and uncomment line 18. Rebuild again.
3. This build will pass.

Sample Output:

```
[2022-10-11T21:52:36.840Z] [+] Building 22.0s (12/12) FINISHED
 => [internal] load build definition from Dockerfile-with-features         0.0s
 => => transferring dockerfile: 1.63kB                                     0.0s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
[2022-10-11T21:52:36.840Z]  => resolve image config for docker.io/docker/dockerfile:1.4               1.0s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io           0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1.4@sha256:9ba7531b  0.0s
 => => resolve docker.io/docker/dockerfile:1.4@sha256:9ba7531bd80fb0a8586  0.0s
 => [internal] load metadata for mcr.microsoft.com/vscode/devcontainers/b  0.2s
 => [context dev_containers_feature_content_source] load .dockerignore     0.0s
 => => transferring dev_containers_feature_content_source: 2B              0.0s
 => [context dev_containers_feature_content_source] load from client       0.0s
 => => transferring dev_containers_feature_content_source: 18.94kB         0.0s
 => [dev_container_auto_added_stage_label 1/1] FROM mcr.microsoft.com/vsc  0.0s
 => => resolve mcr.microsoft.com/vscode/devcontainers/base:0-ubuntu-22.04  0.0s
 => CACHED [dev_containers_ta
[2022-10-11T21:52:36.840Z] rget_stage 1/3] COPY --from=dev_containers_f  0.0s
 => CACHED [dev_containers_target_stage 2/3] RUN cd /tmp/build-features/d  0.0s
 => ERROR [dev_containers_target_stage 3/3] RUN cd /tmp/build-features/a  20.5s
------
 > [dev_containers_target_stage 3/3] RUN cd /tmp/build-features/azure-cli_2 && chmod +x ./devcontainer-features-install.sh && ./devcontainer-features-install.sh:
#0 0.074 ===========================================================================
#0 0.074 Feature       : Azure CLI
#0 0.074 Description   : Installs the Azure CLI along with needed dependencies. Useful for base Dockerfiles that often are missing required install dependencies like gpg.
#0 0.074 Id            : ghcr.io/devcontainers/features/azure-cli
#0 0.074 Version       : 1.0.4
#0 0.074 Documentation : https://github.com/devcontainers/features/tree/main/src/azure-cli
#0 0.074 Options       :
#0 0.074     VERSION="latest"
#0 0.074 ============================================================
[2022-10-11T21:52:36.840Z] ===============
#0 0.084 (*) Installing Azure CLI...
#0 0.089 (*) No pre-built binaries available in apt-cache. Installing via pip3.
#0 0.467 Collecting pipx
#0 0.626   Downloading pipx-1.1.0-py3-none-any.whl (55 kB)
#0 0.663      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 55.4/55.4 KB 3.9 MB/s eta 0:00:00
#0 0.688 Collecting userpath>=1.6.0
#0 0.706   Downloading userpath-1.8.0-py3-none-any.whl (9.0 kB)
#0 0.748 Collecting argcomplete>=1.9.4
#0 0.766   Downloading argcomplete-2.0.0-py2.py3-none-any.whl (37 kB)
#0 0.807 Collecting packaging>=20.0
#0 0.833   Downloading packaging-21.3-py3-none-any.whl (40 kB)
#0 0.844      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.8/40.8 KB 3.8 MB/s eta 0:00:00
[2022-10-11T21:52:36.840Z] #0 0.888 Collecting pyparsing!=3.0.5,>=2.0.2
#0 0.901   Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
#0 0.939      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 98.3/98.3 KB 2.7 MB/s eta 0:00:00
#0 0.972 Collecting click
#0 0.987   Downloading click-8.1.3-py3-none-any.whl (96 kB)
#0 1.029      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.6/96.6 KB 2.2 MB/s eta 0:00:00
#0 1.045 Installing collected packages: pyparsing, click, argcomplete, userpath, packaging, pipx
#0 1.143   WARNING: The script userpath is installed in '/tmp/pip-tmp/bin' which is not on PATH.
#0 1.143   Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
#0 1.184   WARNING: The script pipx is installed in '/tmp/pip-tmp/bin' which is not on PATH.
#0 1.184   Consider adding this directory to PATH or, if you prefer t
[2022-10-11T21:52:36.840Z] o suppress this warning, use --no-warn-script-location.
#0 1.195 Successfully installed argcomplete-2.0.0 click-8.1.3 packaging-21.3 pipx-1.1.0 pyparsing-3.0.9 userpath-1.8.0
#0 1.195 WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
#0 1.348 creating virtual environment...
#0 1.402 installing azure-cli...
#0 20.41 Fatal error from pip prevented installation. Full pip output in file:
#0 20.41     /usr/local/pipx/logs/cmd_2022-10-11_21.52.17_pip_errors.log
#0 20.42
#0 20.42 pip failed to build package:
[2022-10-11T21:52:36.840Z] #0 20.42     psutil
#0 20.42
#0 20.42 Some possibly relevant errors from pip install:
#0 20.42     error: subprocess-exited-with-error
#0 20.42     error: command 'aarch64-linux-gnu-gcc' failed: No such file or directory
#0 20.42     error: legacy-install-failure
#0 20.45
#0 20.45 Error installing azure-cli.
#0 20.47 Could not install azure-cli via pip
#0 20.47 Please provide a valid version for your distribution ubuntu jammy (arm64).
#0 20.47
#0 20.47 Valid versions in current apt-cache
#0 20.49 ERROR: Feature "Azure CLI" (ghcr.io/devcontainers/features/azure-cli) failed to install! Look at the documentation at https://github.com/devcontainers/features/tree/main/src/azure-cli for help troubleshooting this error.
```
