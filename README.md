# Fedora_35_gvt-g






# Working Qemu command

```
LC_ALL=C \
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin \
HOME=/var/lib/libvirt/qemu/domain-5-fedora35-gnome-clone \
XDG_DATA_HOME=/var/lib/libvirt/qemu/domain-5-fedora35-gnome-clone/.local/share \
XDG_CACHE_HOME=/var/lib/libvirt/qemu/domain-5-fedora35-gnome-clone/.cache \
XDG_CONFIG_HOME=/var/lib/libvirt/qemu/domain-5-fedora35-gnome-clone/.config \
MESA_LOADER_DRIVER_OVERRIDE=i965 \
/usr/bin/qemu-system-x86_64 \
-name guest=fedora35-gnome,debug-threads=on \
-machine pc-q35-6.1,accel=kvm,usb=off,vmport=off,dump-guest-core=off,memory-backend=pc.ram \
-cpu host,migratable=on \
-m 12000 \
-object '{"qom-type":"memory-backend-ram","id":"pc.ram","size":12582912000}' \
-overcommit mem-lock=off \
-smp 6,sockets=6,cores=1,threads=1 \
-device virtio-serial-pci,id=virtio-serial0, \
-blockdev '{"driver":"file","filename":"/var/lib/libvirt/images/fedora35-gnome.qcow2","node-name":"libvirt-1-storage","auto-read-only":true,"discard":"unmap"}' \
-blockdev '{"node-name":"libvirt-1-format","read-only":false,"driver":"qcow2","file":"libvirt-1-storage","backing":null}' \
-device virtio-blk-pci,drive=libvirt-1-format,id=virtio-disk0,bootindex=1 \
-device virtserialport,name=org.qemu.guest_agent.0 \
-device virtio-mouse-pci,id=input3 \
-device virtio-keyboard-pci,id=input4 \
-device vfio-pci,id=hostdev0,sysfsdev=/sys/bus/mdev/devices/b591950a-d165-4141-9714-b380f6cd4c9d,display=on,x-igd-opregion=on,ramfb=on,driver=vfio-pci-nohotplug,xres=1440,yres=900 \
-display gtk,gl=on \
-object '{"qom-type":"rng-random","id":"objrng0","filename":"/dev/urandom"}' \
-device virtio-rng-pci,rng=objrng0,id=rng0 \
-object input-linux,id=mouse1,evdev=/dev/input/by-id/usb-04d9_USB_Laser_Game_Mouse-event-mouse \
-object input-linux,id=kbd1,evdev=/dev/input/by-id/usb-Apple__Inc_Apple_Keyboard-event-kbd,grab_all=on,repeat=on \
-vga none \
-net none

```


# Working Libvirt XML

```
<domain xmlns:qemu="http://libvirt.org/schemas/domain/qemu/1.0" type="kvm">
  <name>fedora35-gnome</name>
  <uuid>7c1d2f42-c8bb-44bf-82b0-a804c89a7752</uuid>
  <metadata>
    <libosinfo:libosinfo xmlns:libosinfo="http://libosinfo.org/xmlns/libvirt/domain/1.0">
      <libosinfo:os id="http://fedoraproject.org/fedora/unknown"/>
    </libosinfo:libosinfo>
  </metadata>
  <memory unit="KiB">12288000</memory>
  <currentMemory unit="KiB">12288000</currentMemory>
  <vcpu placement="static">6</vcpu>
  <os>
    <type arch="x86_64" machine="pc-q35-6.1">hvm</type>
    <boot dev="hd"/>
  </os>
  <features>
    <acpi/>
    <apic/>
    <vmport state="off"/>
  </features>
  <cpu mode="host-passthrough" check="partial" migratable="on"/>
  <clock offset="utc">
    <timer name="rtc" tickpolicy="catchup"/>
    <timer name="pit" tickpolicy="delay"/>
    <timer name="hpet" present="no"/>
  </clock>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <pm>
    <suspend-to-mem enabled="no"/>
    <suspend-to-disk enabled="no"/>
  </pm>
  <devices>
    <emulator>/usr/bin/qemu-system-x86_64</emulator>
    <disk type="file" device="disk">
      <driver name="qemu" type="qcow2"/>
      <source file="/var/lib/libvirt/images/fedora35-gnome.qcow2"/>
      <target dev="vda" bus="virtio"/>
      <address type="pci" domain="0x0000" bus="0x04" slot="0x00" function="0x0"/>
    </disk>
    <controller type="usb" index="0" model="qemu-xhci" ports="15">
      <address type="pci" domain="0x0000" bus="0x02" slot="0x00" function="0x0"/>
    </controller>
    <controller type="pci" index="0" model="pcie-root"/>
    <controller type="pci" index="1" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="1" port="0x10"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x4" multifunction="on"/>
    </controller>
    <controller type="pci" index="2" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="2" port="0x11"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x5"/>
    </controller>
    <controller type="pci" index="3" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="3" port="0x12"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x6"/>
    </controller>
    <controller type="pci" index="4" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="4" port="0x13"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x7"/>
    </controller>
    <controller type="pci" index="5" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="5" port="0x14"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x0" multifunction="on"/>
    </controller>
    <controller type="pci" index="6" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="6" port="0x15"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x1"/>
    </controller>
    <controller type="pci" index="7" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="7" port="0x16"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x03" function="0x2"/>
    </controller>
    <controller type="pci" index="8" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="8" port="0x8"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x0" multifunction="on"/>
    </controller>
    <controller type="pci" index="9" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="9" port="0x9"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x1"/>
    </controller>
    <controller type="pci" index="10" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="10" port="0xa"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x2"/>
    </controller>
    <controller type="pci" index="11" model="pcie-root-port">
      <model name="pcie-root-port"/>
      <target chassis="11" port="0xb"/>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x01" function="0x3"/>
    </controller>
    <controller type="virtio-serial" index="0">
      <address type="pci" domain="0x0000" bus="0x03" slot="0x00" function="0x0"/>
    </controller>
    <controller type="sata" index="0">
      <address type="pci" domain="0x0000" bus="0x00" slot="0x1f" function="0x2"/>
    </controller>
    <interface type="network">
      <mac address="52:54:00:87:2c:db"/>
      <source network="default"/>
      <model type="virtio"/>
      <address type="pci" domain="0x0000" bus="0x01" slot="0x00" function="0x0"/>
    </interface>
    <serial type="pty">
      <target type="isa-serial" port="0">
        <model name="isa-serial"/>
      </target>
    </serial>
    <console type="pty">
      <target type="serial" port="0"/>
    </console>
    <channel type="unix">
      <target type="virtio" name="org.qemu.guest_agent.0"/>
      <address type="virtio-serial" controller="0" bus="0" port="1"/>
    </channel>
    <channel type="spicevmc">
      <target type="virtio" name="com.redhat.spice.0"/>
      <address type="virtio-serial" controller="0" bus="0" port="2"/>
    </channel>
    <input type="mouse" bus="ps2"/>
    <input type="keyboard" bus="ps2"/>
    <input type="mouse" bus="virtio">
      <address type="pci" domain="0x0000" bus="0x08" slot="0x00" function="0x0"/>
    </input>
    <input type="keyboard" bus="virtio">
      <address type="pci" domain="0x0000" bus="0x09" slot="0x00" function="0x0"/>
    </input>
    <graphics type="spice">
      <listen type="none"/>
      <image compression="off"/>
      <gl enable="yes" rendernode="/dev/dri/by-path/pci-0000:00:02.0-render"/>
    </graphics>
    <audio id="1" type="spice"/>
    <video>
      <model type="none"/>
    </video>
    <hostdev mode="subsystem" type="mdev" managed="no" model="vfio-pci" display="on">
      <source>
        <address uuid="b591950a-d165-4141-9714-b380f6cd4c9d"/>
      </source>
      <address type="pci" domain="0x0000" bus="0x00" slot="0x02" function="0x0"/>
    </hostdev>
    <redirdev bus="usb" type="spicevmc">
      <address type="usb" bus="0" port="1"/>
    </redirdev>
    <memballoon model="virtio">
      <address type="pci" domain="0x0000" bus="0x05" slot="0x00" function="0x0"/>
    </memballoon>
    <rng model="virtio">
      <backend model="random">/dev/urandom</backend>
      <address type="pci" domain="0x0000" bus="0x06" slot="0x00" function="0x0"/>
    </rng>
  </devices>
  <qemu:commandline>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.display=on"/>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.xres=1920"/>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.yres=1080"/>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.x-igd-opregion=on"/>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.ramfb=on"/>
    <qemu:arg value="-set"/>
    <qemu:arg value="device.hostdev0.driver=vfio-pci-nohotplug"/>
    <qemu:arg value="-object"/>
    <qemu:arg value="input-linux,id=mouse1,evdev=/dev/input/by-id/usb-04d9_USB_Laser_Game_Mouse-event-mouse"/>
    <qemu:arg value="-object"/>
    <qemu:arg value="input-linux,id=kbd1,evdev=/dev/input/by-id/usb-Apple__Inc_Apple_Keyboard-event-kbd,grab_all=on,repeat=on"/>
    <qemu:env name="MESA_LOADER_DRIVER_OVERRIDE" value="i965"/>
  </qemu:commandline>
</domain>

```
