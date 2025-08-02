# Raspberry PI building

## SD card prep

1. Download Latest Crankshaft version
1. Burn to SD Card
1. Turn on Dev_Mode, Set DEV_MODE=1 in /boot/crankshaft/crankshaft_env.sh
1. Set memory split to 16MB for GPU, via raspi-config. This is needed to stop Qt compile from running out of memory

## Full Recompile

1. Boot pi
2. SSH into pi
3. add SSH public key
```bash
   mkdir .ssh
   touch .ssh/authorized_keys
   chmod 644 .ssh/authorized_keys
   chown pi:pi .ssh/authorized_keys
```
4. Configure nameserver
```bash
   sudo nano /etc/resolv.conf
   nameserver 8.8.8.8
```
5. Update Buster
```bash
   sudo apt update -y
   sudo apt upgrade -y
   sudo apt autoremove -y
```
6. Setup Build Environment
```bash
mkdir ~/opencardev
cd ~/opencardev
git clone https://github.com/elarchenko/prebuilts.git prebuilts
cd prebuilts/buildsystem
./1_prepare_build_system.sh
```
7. Build
```bash
./3_build_ilclient.sh
./4_build_qt_latest.sh
./5_build_openauto.sh
./99_copy_compiled_files.sh
cd ..
./update_binaries.sh
```
