# my nssm setup

Here's my documentation for how I set up [nssm](https://nssm.cc/) on my Windows machines.

## Prerequisites

- Install nssm with scoop:

  ```shell
  scoop bucket add main
  scoop install main/nssm
  ```

## Services

[!IMPORTANT]\
Any nssm command that sets `ObjectName` should replace the
asterisks with the true password for that user. It may be helpful to edit the
commands in a text editor.

### unftp

This provides an ftp server that [my printer](https://github.com/t-mart/brother-mfc-7860dw-setup) can upload documents/photos to.

```shell
nssm.exe install unftp C:\Users\tim\.cargo\bin\unftp.exe
nssm.exe set unftp AppParameters ^"--bind-address 0.0.0.0:21 --bind-address-http 0.0.0.0:8021 --auth-type anonymous --root-dir ^\^"C:^\Users^\tim^\Desktop^\scans^\^"^"
nssm.exe set unftp AppDirectory C:\Users\tim\.cargo\bin
nssm.exe set unftp AppExit Default Restart
nssm.exe set unftp DisplayName unftp
nssm.exe set unftp ObjectName .\tim "****"
nssm.exe set unftp Start SERVICE_AUTO_START
nssm.exe set unftp Type SERVICE_WIN32_OWN_PROCESS
```

## Adding new services to this list

Use the dump subcommand:

```shell
nssm dump <servicename>
```
