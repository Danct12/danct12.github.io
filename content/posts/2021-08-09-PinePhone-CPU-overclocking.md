---
date: "2021-08-09T00:00:00Z"
title: How to overclock (or underclock) the PinePhone CPU
categories:
- Tutorials
tags:
- overclock
- underclock
- linux
- pinephone
- cpu
- allwinner
- device tree
---

The CPU in the PinePhone is decent enough for most tasks, but not all people think the same way and will look into overclocking to get the maximum performance.

**Overclocking is a very risky process as it makes the phone run hotter and too much overvolting might fry the SoC. I won't be responsible for any damage that has caused, you've been warned.**

**This guide is aimed toward experienced users, requiring the user to compile their own kernel.**

First, clone the [megi's kernel source code](https://github.com/megous/linux/tree/orange-pi-5.13), this is a kernel that is used on many PinePhone distros. On some distribution such as Mobian uses their own kernel, so check your vendor first!

*Some distribution might include additional patches for better support, so you should apply them after the kernel has cloned.*

After ther kernel cloned (and applied the additional patches), open [arch/arm64/boot/dts/allwinner/sun50i-a64-pinephone.dtsi](https://github.com/megous/linux/blob/orange-pi-5.13/arch/arm64/boot/dts/allwinner/sun50i-a64-pinephone.dtsi) and look for:

```
...
&cpu0 {
	cpu-supply = <&reg_dcdc2>;
};

&cpu1 {
	cpu-supply = <&reg_dcdc2>;
};

&cpu2 {
	cpu-supply = <&reg_dcdc2>;
};

&cpu3 {
	cpu-supply = <&reg_dcdc2>;
};
...
```

The CPU power is supplied through reg_dcdc2, so what is it? Let's search for it.

```
...
&reg_dcdc2 {
	regulator-always-on;
	regulator-min-microvolt = <1000000>;
	regulator-max-microvolt = <1300000>;
	regulator-name = "vdd-cpux";
};
...
```

Aha! This is the min/max voltage for the CPU in microvolt, you can change this to the desired value. **Keep in mind that too much voltage can fry the chip!**. I want to underclock the SoC, so I'll change the `regulator-min-microvolt` value to 400000 (0.4V)

Once that's done, let's take a look at [arch/arm64/boot/dts/allwinner/sun50i-a64-cpu-opp.dtsi](https://github.com/megous/linux/blob/orange-pi-5.13/arch/arm64/boot/dts/allwinner/sun50i-a64-cpu-opp.dtsi).

```
/ {
	cpu0_opp_table: opp_table0 {
		compatible = "operating-points-v2";
		opp-shared;

		opp-648000000 {
			opp-hz = /bits/ 64 <648000000>;
			opp-microvolt = <1040000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-816000000 {
			opp-hz = /bits/ 64 <816000000>;
			opp-microvolt = <1100000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-912000000 {
			opp-hz = /bits/ 64 <912000000>;
			opp-microvolt = <1120000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-960000000 {
			opp-hz = /bits/ 64 <960000000>;
			opp-microvolt = <1160000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-1008000000 {
			opp-hz = /bits/ 64 <1008000000>;
			opp-microvolt = <1200000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-1056000000 {
			opp-hz = /bits/ 64 <1056000000>;
			opp-microvolt = <1240000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-1104000000 {
			opp-hz = /bits/ 64 <1104000000>;
			opp-microvolt = <1260000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};

		opp-1152000000 {
			opp-hz = /bits/ 64 <1152000000>;
			opp-microvolt = <1300000>;
			clock-latency-ns = <244144>; /* 8 32k periods */
		};
	};
};
```

These are CPU operating points, which is what handling our clocks. We'll add a new node for the new clock speed, this is up to you to experiment with.

This is the configuration that I find to be stable for me:
```
opp-48000000 {
        opp-hz = /bits/ 64 <48000000>;
        opp-microvolt = <780000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};

opp-100000000 {
        opp-hz = /bits/ 64 <100000000>;
        opp-microvolt = <790000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};

opp-200000000 {
        opp-hz = /bits/ 64 <200000000>;
        opp-microvolt = <800000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};

opp-408000000 {
        opp-hz = /bits/ 64 <408000000>;
        opp-microvolt = <830000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};

opp-492000000 {
        opp-hz = /bits/ 64 <492000000>;
        opp-microvolt = <860000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};

opp-552000000 {
        opp-hz = /bits/ 64 <552000000>;
        opp-microvolt = <900000>;
        clock-latency-ns = <244144>; /* 8 32k periods */
};
```

Once that's done, you can compile the dtbs:
```
ARCH=arm64 make dtbs
```

The DTB should be in `arch/arm64/boot/dts/allwinner/sun50i-a64-pinephone-*.dtb`, you can now transfer them to your device and overwrite the old dtb (make sure to back it up first) then reboot.

If your device crashes on boot or being unstable, try to experiment with your configuration a bit more until you get a stable setup.

Day 5 of #100DaysToOffload.
