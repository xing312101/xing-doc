# Maximo

## pre-install
> Check supported os version first.

#### download installer
* IBM Maximo Asset Management V7.6.1 Linux 64 Multilingual
    - MAM_7.6.1.0_LINUX64.tar.gz

* IBM Maximo Middleware Installer, DB2 11.1 Linux X86-64 Multilingual (CNVK6ML)
    - Middl_Inst_DB2_111_Linux_x86-64.tar.gz
* IBM Maximo Middleware Installer, WebSphere Application Server 9.0 Unix 64
    - Middl_Inst_WAS_90_1of3_Unix.tar.gz
    - Middl_Inst_WAS_90_2of3_Unix.tar.gz
    - Middl_Inst_WAS_90_3of3_Unix.tar.gz

#### unzip files
```
## 解壓縮路徑隨意
$ mkdir /opt/source/instl
$ cd /opt/source

$ tar ./instl -xzvf MAM_7.6.1.0_LINUX64.tar.gz									# AP, DB Server
$ tar ./instl -xzvf Middl_Inst_DB2_111_Linux_x86-64.tar.gz			# DB Server
$ tar ./instl -xzvf Middl_Inst_WAS_90_1of3_Unix.tar.gz					# AP Server
$ tar ./instl -xzvf Middl_Inst_WAS_90_2of3_Unix.tar.gz					# AP Server
$ tar ./instl -xzvf Middl_Inst_WAS_90_3of3_Unix.tar.gz					# AP Server

# 不需要解壓縮 fix patch
# $ mkdir /opt/source/fixpack
# $ unzip TPAE_7610_IFIX.20190404-1532.im.zip -d ./fixpack

```

## install  IBM Installation Manager
```
$ cd /opt/source/instl/Install/IM/installer.linux.x86_64

# 安裝 IBM Installation Manager
$ ./installc -acceptLicense

The application path:
/opt/IBM/InstallationManager/eclipse


# May some library need install
Gtk-Message: Failed to load module "canberra-gtk-module"
$ sudo apt install libcanberra-gtk-module libcanberra-gtk3-module

```
## Run IBMIM to install
```
run /opt/IBM/InstallationManager/eclipse/IBMIM
- select repositories in /opt/source/instl/install:
	 1. mwi_madt_DB2AWSv11.1.0.0_images/repository.config
	 2. ConfigToolRepository/repository.config
	 3. ProductInstallerRepository/repository.config
	 4. TPAEInstallerRepository/repository.config
	 5. MWInstallerRepository/repository.config
	 6. mwi_madt_WASv9.0.0.7_images/repository.config

```
### Install IBM DB2
```
- select "IBM DB2 Advanced Workgroup Server Edition"
```


#### Fix Install Error

 • CTGIN8273E : Required ulimit : The File Size Limit must be set to 'unlimited' (-1) and the File Descriptor Limit must be set to 'unlimited' (-1) or at least 8192.
 Value Reported : 1024
```
fix:
 vim /etc/security/limits.conf

root            hard    nofile  10000
root            soft    nofile  10000
```

 • CTGIN8267E : SELinux Consideration : SELinux is enabled
```
Method 1:
$ setenforce 0

Method 2:
$ export BYPASS_PRS=True
```

## Install Maximo
```
select:
IBM Maximo Asset Management
IBM Maximo Tivoli Process Automation Engine
IBM Tivoli’s process automation suite configuration tool for Websphere Application Server
IBM HTTP Server for WebSphere Application Server
IBM WebSphere Application Server Network Deployment
Web Server Plug-ins for IBM WebSphere Application Server
WebSphere Customization Toolbox
IBM SDK, Java Technology Edition, Version 8
```

## WebSphere Setting
```
Open
"Tivoli's Process Automation Engine Configuration UI"
/opt/IBM/ConfigTool/ConfigUI
```

### Prepare WebSphere Application Server for configuration
```
setup admin password
```


### Configure a new Administrative Workstation to point to an existing Asset Management deployment
....



