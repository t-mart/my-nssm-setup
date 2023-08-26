# my nssm setup

Here's my documentation for how I set up [nssm](https://nssm.cc/) on my Windows machines.

## Prerequisites

- Install nssm with scoop:

  ```shell
  scoop bucket add main
  scoop install main/nssm
  ```

## Services

> **Important**
> Any nssm command that sets `ObjectName` should replace the
> asterisks with the true password for that user. It may be helpful to edit the
> commands in a text editor.

### unftp

Install unftp with:

```shell
cargo install unftp
```

Then install the service with:

```shell
nssm install unftp C:\Users\tim\.cargo\bin\unftp.exe
nssm set unftp AppParameters "--bind-address 0.0.0.0:21 --bind-address-http 0.0.0.0:8021 --auth-type anonymous --root-dir ""C:/Users/tim/Desktop/scans/"" -v"
nssm set unftp AppDirectory C:\Users\tim\.cargo\bin
nssm set unftp AppExit Default Restart
nssm set unftp DisplayName unftp
nssm set unftp ObjectName .\tim "****"
nssm set unftp Start SERVICE_AUTO_START
nssm set unftp Type SERVICE_WIN32_OWN_PROCESS
```

### AdGuard Home

Install AdGuard Home with:

```shell
# note this is in my own bucket
scoop bucket add t-mart https://github.com/t-mart/t-mart-scoop-bucket
scoop install t-mart/adguard-home
```

Then install the service with:

```shell
nssm install adguard-home C:\Users\tim\scoop\apps\adguard-home\current\AdGuardHome.exe
nssm set adguard-home AppDirectory C:\Users\tim\scoop\apps\adguard-home\current
nssm set adguard-home AppExit Default Restart
nssm set adguard-home DisplayName adguard-home
nssm set adguard-home ObjectName .\tim "****"
nssm set adguard-home Start SERVICE_AUTO_START
nssm set adguard-home Type SERVICE_WIN32_OWN_PROCESS
```

### stash

Install stash with:

```shell
scoop install versions/stash-dev
```

Then install the service with:

```shell
nssm install stash C:\Users\tim\scoop\apps\stash-dev\current\stash-win.exe
nssm set stash AppDirectory C:\Users\tim\scoop\apps\stash-dev\current
nssm set stash AppExit Default Restart
nssm set stash DisplayName stash
nssm set stash ObjectName .\tim "****"
nssm set stash Start SERVICE_AUTO_START
nssm set stash Type SERVICE_WIN32_OWN_PROCESS
```

## Adding new services to this list

Use the dump subcommand:

```shell
nssm dump <servicename>
```

> **Note**
> `nssm dump` inserts weird characters in its output that I've had trouble with it. For any quotes that need to appear in values, just use `""` (two quotes).
