# OCI_CLI_Ubuntu_24.04_LTS
## Install the Oracle Cloud Infrastructure CLI on Ubuntu 24.04 LTS

### This is a short post about installing/configuring the Oracle Cloud Infrastructure (OCI) Command Line Interface (CLI) on Ubuntu 24.04 LTS.

**Creating a virtual environment:**
The first step is to create a virtual environment to prevent the OCI CLI’s dependencies from messing up my python installation.

```
mkdir -p ~/development/python && cd ~/development/python
sudo apt install python3.8-venv
python3 -m venv oracle-cli
```
With the venv in place you need to activate it. This is a crucial step! Don’t forget to run it

```source oracle-cli/bin/activate```
As soon as the venv is activated you’ll notice its name has become a part of the prompt.

**Downloading the OCI CLI 
**
The next step is to download the latest OCI CLI release from [Github](https://github.com/oracle/oci-cli/releases/tag/v3.50.1). At the time of writing, version 3.50.1 was the most current. Ensure you load the vanilla release, e.g. oci-cli-release.zip, not one of the distribution-specific ones. These are to be used for offline installation.
```
curl -L "https://github.com/oracle/oci-cli/releases/download/v3.50.1/oci-cli-3.50.1.zip" -o /tmp/oci-cli-3.50.1.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0
100  136M  100  136M    0     0  1342k      0  0:01:44  0:01:44 --:--:-- 1565k
```
> [!TIP]
> Unzip the release temporarily and begin the installation by invoking pip using the “whl” file in the freshly unzipped directory. 



> [!WARNING]
> Just to make sure I always double-check I’m using the pip executable in the virtual environment before proceeding.

> [!IMPORTANT]
> If you want to complete all tasks at once, just open a terminal and run the command [
> bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)" ]



You’ll notice additional packages are pulled into the virtual environment by the setup routine. As always, exercise care when using external packages. An [offline installation](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/climanualinst.htm#InstallingCLI_Offline) is available as well if your security requirements mandate it.
At the end of the process, you have a working installation of the command line interface.

**Configuration**
Before you can use the CLI you need to provide a configuration file. The default location is ~/.oci, which I’ll use as well.

```mkdir ~/.oci && cd ~/.oci```

Inside of this directory, you need to [create a config file](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm#File_Name_and_Location); the example below is taken from the documentation and should provide a starting point.
```
[DEFAULT]
user=ocid1.user.oc1..<unique_ID>
fingerprint=<your_fingerprint>
key_file=~/.oci/oci_api_key.pem
tenancy=ocid1.tenancy.oc1..<unique_ID>
region=us-ashburn-1
```


Make sure to update the values accordingly. Should you be unsure about the user OCID and/or API signing key to use, yum may go through the [documentation](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm) for instructions. Next time you invoke the CLI the DEFAULT configuration will be used. 




> [!NOTE]
> Logs 
```
root@nasim-desktop:~# mkdir -p ~/development/python && cd ~/development/python
root@nasim-desktop:~/development/python# apt install python3.8-venv
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libpython3.8-minimal libpython3.8-stdlib python3.8 python3.8-distutils
  python3.8-lib2to3 python3.8-minimal
Suggested packages:
  binfmt-support
The following NEW packages will be installed:
  libpython3.8-minimal libpython3.8-stdlib python3.8 python3.8-distutils
  python3.8-lib2to3 python3.8-minimal python3.8-venv
0 upgraded, 7 newly installed, 0 to remove and 3 not upgraded.
Need to get 7,551 kB of archives.
After this operation, 22.5 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 libpython3.8-minimal amd64 3.8.20-1+noble1 [745 kB]
Get:2 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 python3.8-minimal amd64 3.8.20-1+noble1 [1,791 kB]
Get:3 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 libpython3.8-stdlib amd64 3.8.20-1+noble1 [1,771 kB]
Get:4 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 python3.8 amd64 3.8.20-1+noble1 [395 kB]
Get:5 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 python3.8-lib2to3 all 3.8.20-1+noble1 [81.6 kB]
Get:6 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 python3.8-distutils all 3.8.20-1+noble1 [148 kB]
Get:7 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu noble/main amd64 python3.8-venv amd64 3.8.20-1+noble1 [2,619 kB]
Fetched 7,551 kB in 13s (591 kB/s)                                             
Selecting previously unselected package libpython3.8-minimal:amd64.
(Reading database ... 199934 files and directories currently installed.)
Preparing to unpack .../0-libpython3.8-minimal_3.8.20-1+noble1_amd64.deb ...
Unpacking libpython3.8-minimal:amd64 (3.8.20-1+noble1) ...
Selecting previously unselected package python3.8-minimal.
Preparing to unpack .../1-python3.8-minimal_3.8.20-1+noble1_amd64.deb ...
Unpacking python3.8-minimal (3.8.20-1+noble1) ...
Selecting previously unselected package libpython3.8-stdlib:amd64.
Preparing to unpack .../2-libpython3.8-stdlib_3.8.20-1+noble1_amd64.deb ...
Unpacking libpython3.8-stdlib:amd64 (3.8.20-1+noble1) ...
Selecting previously unselected package python3.8.
Preparing to unpack .../3-python3.8_3.8.20-1+noble1_amd64.deb ...
Unpacking python3.8 (3.8.20-1+noble1) ...
Selecting previously unselected package python3.8-lib2to3.
Preparing to unpack .../4-python3.8-lib2to3_3.8.20-1+noble1_all.deb ...
Unpacking python3.8-lib2to3 (3.8.20-1+noble1) ...
Selecting previously unselected package python3.8-distutils.
Preparing to unpack .../5-python3.8-distutils_3.8.20-1+noble1_all.deb ...
Unpacking python3.8-distutils (3.8.20-1+noble1) ...
Selecting previously unselected package python3.8-venv.
Preparing to unpack .../6-python3.8-venv_3.8.20-1+noble1_amd64.deb ...
Unpacking python3.8-venv (3.8.20-1+noble1) ...
Setting up libpython3.8-minimal:amd64 (3.8.20-1+noble1) ...
Setting up python3.8-lib2to3 (3.8.20-1+noble1) ...
Setting up python3.8-minimal (3.8.20-1+noble1) ...
Setting up python3.8-distutils (3.8.20-1+noble1) ...
Setting up libpython3.8-stdlib:amd64 (3.8.20-1+noble1) ...
Setting up python3.8 (3.8.20-1+noble1) ...
Setting up python3.8-venv (3.8.20-1+noble1) ...
Processing triggers for gnome-menus (3.36.0-1.1ubuntu3) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for desktop-file-utils (0.27-2build1) ...
root@nasim-desktop:~/development/python# python3 -m venv oracle-cli
root@nasim-desktop:~/development/python# source oracle-cli/bin/activate
(oracle-cli) root@nasim-desktop:~/development/python# curl -L "https://github.com/oracle/oci-cli/releases/download/v3.50.1/oci-cli-3.50.1.zip" -o /tmp/oci-cli-3.50.1.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0
100  136M  100  136M    0     0  1342k      0  0:01:44  0:01:44 --:--:-- 1565k
(oracle-cli) root@nasim-desktop:~/development/python# pip install /tmp/oci-cli-3.50.1/oci-cli/oci_cli-3.50.1-py3-none-any.whl
Processing /tmp/oci-cli-3.50.1/oci-cli/oci_cli-3.50.1-py3-none-any.whl
Collecting oci==2.138.1 (from oci-cli==3.50.1)
  Downloading oci-2.138.1-py3-none-any.whl.metadata (5.3 kB)
Collecting arrow>=1.0.0 (from oci-cli==3.50.1)
  Downloading arrow-1.3.0-py3-none-any.whl.metadata (7.5 kB)
Collecting certifi (from oci-cli==3.50.1)
  Downloading certifi-2024.8.30-py3-none-any.whl.metadata (2.2 kB)
Collecting click==8.0.4 (from oci-cli==3.50.1)
  Downloading click-8.0.4-py3-none-any.whl.metadata (3.2 kB)
Collecting cryptography<46.0.0,>=3.2.1 (from oci-cli==3.50.1)
  Downloading cryptography-43.0.3-cp39-abi3-manylinux_2_28_x86_64.whl.metadata (5.4 kB)
Collecting jmespath==0.10.0 (from oci-cli==3.50.1)
  Downloading jmespath-0.10.0-py2.py3-none-any.whl.metadata (8.0 kB)
Collecting python-dateutil<3.0.0,>=2.5.3 (from oci-cli==3.50.1)
  Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl.metadata (8.4 kB)
Collecting pytz>=2016.10 (from oci-cli==3.50.1)
  Downloading pytz-2024.2-py2.py3-none-any.whl.metadata (22 kB)
Collecting six>=1.15.0 (from oci-cli==3.50.1)
  Downloading six-1.16.0-py2.py3-none-any.whl.metadata (1.8 kB)
Collecting terminaltables==3.1.10 (from oci-cli==3.50.1)
  Downloading terminaltables-3.1.10-py2.py3-none-any.whl.metadata (3.5 kB)
Collecting pyOpenSSL<25.0.0,>=17.5.0 (from oci-cli==3.50.1)
  Downloading pyOpenSSL-24.2.1-py3-none-any.whl.metadata (13 kB)
Collecting PyYAML<=6.0.1,>=5.4 (from oci-cli==3.50.1)
  Downloading PyYAML-6.0.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.1 kB)
Collecting prompt-toolkit<=3.0.43,>=3.0.38 (from oci-cli==3.50.1)
  Downloading prompt_toolkit-3.0.43-py3-none-any.whl.metadata (6.5 kB)
Collecting circuitbreaker<3.0.0,>=1.3.1 (from oci==2.138.1->oci-cli==3.50.1)
  Downloading circuitbreaker-2.0.0-py2.py3-none-any.whl.metadata (7.7 kB)
Collecting types-python-dateutil>=2.8.10 (from arrow>=1.0.0->oci-cli==3.50.1)
  Downloading types_python_dateutil-2.9.0.20241003-py3-none-any.whl.metadata (1.9 kB)
Collecting cffi>=1.12 (from cryptography<46.0.0,>=3.2.1->oci-cli==3.50.1)
  Downloading cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.5 kB)
Collecting wcwidth (from prompt-toolkit<=3.0.43,>=3.0.38->oci-cli==3.50.1)
  Downloading wcwidth-0.2.13-py2.py3-none-any.whl.metadata (14 kB)
Collecting pycparser (from cffi>=1.12->cryptography<46.0.0,>=3.2.1->oci-cli==3.50.1)
  Downloading pycparser-2.22-py3-none-any.whl.metadata (943 bytes)
Downloading click-8.0.4-py3-none-any.whl (97 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 97.5/97.5 kB 6.9 MB/s eta 0:00:00
Downloading jmespath-0.10.0-py2.py3-none-any.whl (24 kB)
Downloading oci-2.138.1-py3-none-any.whl (28.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 28.4/28.4 MB 14.1 MB/s eta 0:00:00
Downloading terminaltables-3.1.10-py2.py3-none-any.whl (15 kB)
Downloading arrow-1.3.0-py3-none-any.whl (66 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 66.4/66.4 kB 5.7 MB/s eta 0:00:00
Downloading cryptography-43.0.3-cp39-abi3-manylinux_2_28_x86_64.whl (4.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.0/4.0 MB 8.9 MB/s eta 0:00:00
Downloading prompt_toolkit-3.0.43-py3-none-any.whl (386 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 386.1/386.1 kB 8.4 MB/s eta 0:00:00
Downloading pyOpenSSL-24.2.1-py3-none-any.whl (58 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 58.4/58.4 kB 8.5 MB/s eta 0:00:00
Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl (229 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 229.9/229.9 kB 8.9 MB/s eta 0:00:00
Downloading pytz-2024.2-py2.py3-none-any.whl (508 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 508.0/508.0 kB 9.2 MB/s eta 0:00:00
Downloading PyYAML-6.0.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (724 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 725.0/725.0 kB 7.6 MB/s eta 0:00:00
Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Downloading certifi-2024.8.30-py3-none-any.whl (167 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 167.3/167.3 kB 7.1 MB/s eta 0:00:00
Downloading cffi-1.17.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (479 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 479.4/479.4 kB 7.5 MB/s eta 0:00:00
Downloading circuitbreaker-2.0.0-py2.py3-none-any.whl (7.6 kB)
Downloading types_python_dateutil-2.9.0.20241003-py3-none-any.whl (9.7 kB)
Downloading wcwidth-0.2.13-py2.py3-none-any.whl (34 kB)
Downloading pycparser-2.22-py3-none-any.whl (117 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 117.6/117.6 kB 7.6 MB/s eta 0:00:00
Installing collected packages: wcwidth, pytz, circuitbreaker, types-python-dateutil, terminaltables, six, PyYAML, pycparser, prompt-toolkit, jmespath, click, certifi, python-dateutil, cffi, cryptography, arrow, pyOpenSSL, oci, oci-cli
Successfully installed PyYAML-6.0.1 arrow-1.3.0 certifi-2024.8.30 cffi-1.17.1 circuitbreaker-2.0.0 click-8.0.4 cryptography-43.0.3 jmespath-0.10.0 oci-2.138.1 oci-cli-3.50.1 prompt-toolkit-3.0.43 pyOpenSSL-24.2.1 pycparser-2.22 python-dateutil-2.9.0.post0 pytz-2024.2 six-1.16.0 terminaltables-3.1.10 types-python-dateutil-2.9.0.20241003 wcwidth-0.2.13
(oracle-cli) root@nasim-desktop:~/development/python# mkdir ~/.oci && cd ~/.oci
(oracle-cli) root@nasim-desktop:~/.oci# vim config
```
