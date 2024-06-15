## Установка Wireshark
1. Установить зависимости
~~~
sudo apt install libc-ares-dev libgcrypt20-dev libglib2.0-dev glib-networking
~~~
2. Скрипт сборки **build_wireshark.py**
~~~
import os
import subprocess
# VERSIONS
kLibGpgError="libgpg-error-1.37"
kLibCrypt="libgcrypt-1.10.2"
kWireshark="wireshark"
# CUR DIR
kCurDir = os.path.abspath(os.curdir)

os.chdir(kCurDir)
    if not os.path.exists(kWireshark):
        subprocess.run(["git","clone","https://github.com/wireshark/wireshark.git",kWireshark])
        os.chdir(kWireshark)
        if not os.path.exists("build"):
        os.mkdir("build")
        subprocess.run(["cmake","-S",kCurDir+"/"+kWireshark,"-B",kCurDir+"/"+kWireshark+"/build",
                "-G Unix Makefiles",
                "-DCMAKE_BUILD_TYPE=Release",
                "-DBUILD_tshark=OFF",
                "-DBUILD_rawshark=OFF",
                "-DBUILD_dumpcap=OFF",
                "-DBUILD_text2pcap=OFF",
                "-DBUILD_mergecap=OFF",
                "-DBUILD_reordercap=OFF",
                "-DBUILD_editcap=OFF",
                "-DBUILD_capinfos=OFF",
                "-DBUILD_captype=OFF",
                "-DBUILD_randpkt=OFF",
                "-DBUILD_dftest=OFF",
                "-DBUILD_dcerpcidl2wrs=OFF",
                "-DBUILD_androiddump=OFF",
                "-DBUILD_sshdump=OFF",
                "-DBUILD_ciscodump=OFF",
                "-DBUILD_dpauxmon=OFF",
                "-DBUILD_randpktdump=OFF",
                "-DBUILD_wifidump=OFF",
        "-DBUILD_sharkd=OFF",
        "-DBUILD_wireshark=OFF",
        "-DBUILD_udpdump=OFF",
        "-DBUILD_mmdbresolve=OFF",
        "-DENABLE_AIRPCAP=OFF",
        "-DENABLE_PLUGINS=OFF",
        "-DENABLE_KERBEROS=OFF",
        "-DENABLE_SBC=OFF=OFF",
        "-DENABLE_SPANDSP=OFF",
        "-DENABLE_BCG729=OFF",
        "-DENABLE_ILBC=OFF",
        "-DENABLE_LIBXML2=OFF",
        "-DENABLE_OPUS=OFF",
        "-DENABLE_SINSP=OFF"])
        subprocess.run(["cmake","--build",kCurDir+"/"+kWireshark+"/build"])
~~~
