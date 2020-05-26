# HDMI to DP adapter for imx8mq

The imx8mq can output HDMI 2.0a or eDP/DP via it's HDMI TX. 
In order to test DisplayPort with a board that's designed
for HDMI one can use this adapter board. For this to work
you need to

- remove pull downs from the HDMI lanes. That's R1901-R1908 on the [Librem5 devkit][]
- use the DisplayPort instead of the HDMI firmware in uboot
  from https://www.nxp.com/lgfiles/NMG/MAD/YOCTO/firmware-imx-8.7.bin
- configure the Linux kernel for DP instead of HDMI for the cadence bridge
  as used in NXPs BSP:
  
```
&hdmi {
        compatible = "cdn,imx8mq-dp";
        lane-mapping = <0xc6>;
        status = "okay";
        port@1 {
                hdmi_in: endpoint {
                        remote-endpoint = <&dcss_out>;
                };
        };
};
```

The schematics for this kind of adapter were initially pubilshed by Bernhard
Fink from NXPs forum at https://community.nxp.com/thread/491629 .

[Librem5 devkit]: https://source.puri.sm/Librem5/dvk-mx8m-bsb
