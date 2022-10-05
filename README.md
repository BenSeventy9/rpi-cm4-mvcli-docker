# Instructions and how to use marvell command line interface made for amd64 on arm64 with box64 docker container
## Hardware
- Raspberry Pi CM4 and IO Board with PCIE Connector
- Marvell® 88SE9220/9230 PCIe to SATA 6Gb/s Controllers RAID 0/1/10 HyperDuo
- Tested: 88SE9230
- Untested: 88SE9220
## Prerequisites
- Docker
- 64bit OS
# Download mvcli and usage instructions
- Found here: https://www.dell.com/support/home/de-ch/drivers/driversdetails?driverid=67hr5
### Download:
```
wget https://dl.dell.com/FOLDER04572610M/1/mvcli%204.1.13.31_A01.zip
unzip 'mvcli 4.1.13.31_A01.zip'
mkdir mvclidocker
cd mvclidocker
cp ../'mvcli 4.1.13.31_A01'/x64/cli/mvcli $(pwd)
chmod 755 $(pwd)/mvcli
cp ../'mvcli 4.1.13.31_A01'/x64/cli/libmvraid.so $(pwd)
```
### Usage:
Run:
```
sudo docker run -it --name mvcli --rm -e BOX64_LOG=0 -e BOX64_LD_LIBRARY_PATH=/library --privileged -v $(pwd):/binary  -v $(pwd):/library weilbyte/box:debian-11 /binary/mvcli
```
Output:
```
~/mvclidocker $ sudo docker run -it --name mvcli --rm -e BOX64_LOG=0 -e BOX64_LD_LIBRARY_PATH=/library --privileged -v $(pwd):/binary  -v $(pwd):/library weilbyte/box:debian-11 /binary/mvcli
Box64 with Dynarec v0.1.9 5336524 built on Jul  3 2022 02:42:10
SG driver version 3.5.36.
CLI Version: 4.1.13.31   RaidAPI Version: 5.0.13.1071
Welcome to RAID Command Line Interface.

>
```
Help command:
```
help
```
Output:
```
> help

Legend:
  [options] - the options within [] are optional.
  <x|y|z>   - choose one of the x, y or z.
  [<x|y|z>] - choose none or one of the x, y or z.

Abbreviation:
    VD  - Virtual Disk,   Array  - Disk Array
    PD  - Physical Disk,  BGA - BackGround Activity

Type '-output [filename]' to output to a file.
Type 'help' to display this page.
Type 'help command' to display the help page of 'command'.
Type 'command -h' to display help for 'command'.

Command name is not case sensitive and may be abbreviated if the
abbreviation is unique. Most commands support both short (-) and
long (--) options.Long option names may be abbreviated if the abbreviation
is unique. A long option may take a parameter of the form '--arg=param'
or '--arg param'. Option name is case sensitive, option parameter is not.

COMMAND   BRIEF DESCRIPTION
-----------------------------------------------------------------
?            :Get brief help for all commands.
help         :Get brief help for all commands or detail help for one command.
rebuild      :Start, stop, pause, resume rebuilding VD.
smart        :Display the smart info of physical disk.
flash        :Update, backup or erase flash image and erase hba or pd page.
enc          :Get enclosure, enclosure element or enclosure config information.
adapter      :Default adapter the following CLI commands refers to.
create       :Create virtual disk.
delete       :Delete virtual disk or spare drive.
event        :Get the current events.
get          :Get configuration information of VD, PD, Array, HBA or Driver.
info         :Display adapter(hba), virtual disk(vd), disk array,
              physical disk(pd), Port multiplexer(pm), expander(exp),
              block disk(blk) or spare drive information.
set          :Set configuration parameters of VD, PD or HBA.
import       :Import a virtual disk.
locate       :Locate the specified PD.
report       :report a conflicted virtual disk to OS.
devmap       :Map device ID to device magic number in the OS.

>
```
This command is also possible if you don't need shell mode support:
```
sudo docker run -it --name mvcli --rm -e BOX64_LOG=0 -e BOX64_LD_LIBRARY_PATH=/library --privileged -v $(pwd):/binary  -v $(pwd):/library weilbyte/box:debian-11 /binary/mvcli help
```
