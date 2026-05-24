# Linux G1A

This is a fork of the [linux-mainline](https://aur.archlinux.org/packages/linux-mainline) package that includes support for the webcam on AMD G1A based laptops. Specifically, inclusion of upstream patches and addition of the CONFIG_AMD_ISP4=m kernel configuration option. You will need recent kernel firmware (newer than 20250825) which [linux-firmware-git](https://aur.archlinux.org/packages/linux-firmware-git) provides and the following mkinitcpio.conf change `FILES=(/usr/lib/firmware/amdgpu/isp_4_1_1.bin.zst)`. With this complete, `v4l2-ctl --all` should show the webcam.

Special thanks to the [Level1Techs Forum](https://forum.level1techs.com/t/the-ultimate-arch-secureboot-guide-for-ryzen-ai-max-ft-hp-g1a-128gb-8060s-monster-laptop/230652) and [xGloooM](https://github.com/iglooom/AMD-ISP4-kernel-patches).


## Notes

I added the following firmware blobs manually to the initramfs:

```
/usr/lib/firmware/amdgpu/isp_4_1_1.bin.zst
/usr/lib/firmware/mediatek/mt7925/BT_RAM_CODE_MT7925_1_1_hdr.bin.zst
/usr/lib/firmware/mediatek/mt7925/WIFI_MT7925_PATCH_MCU_1_1_hdr.bin.zst
/usr/lib/firmware/mediatek/mt7925/WIFI_RAM_CODE_MT7925_1_1.bin.zst
```

I haven't tried if it works without doing this. 


If you are using `mkinitcpio` add the following to `/etc/mkinitcpio.conf`:

```
FILES=(
    /usr/lib/firmware/amdgpu/isp_4_1_1.bin.zst
    /usr/lib/firmware/mediatek/mt7925/BT_RAM_CODE_MT7925_1_1_hdr.bin.zst
    /usr/lib/firmware/mediatek/mt7925/WIFI_MT7925_PATCH_MCU_1_1_hdr.bin.zst
    /usr/lib/firmware/mediatek/mt7925/WIFI_RAM_CODE_MT7925_1_1.bin.zst
)
```


If you are using dracut, you can do it by creating a file `/etc/dracut.conf.d/g1a.conf`:

```
install_items+=" /usr/lib/firmware/amdgpu/isp_4_1_1.bin.zst "
install_items+=" /usr/lib/firmware/mediatek/mt7925/BT_RAM_CODE_MT7925_1_1_hdr.bin.zst "
install_items+=" /usr/lib/firmware/mediatek/mt7925/WIFI_MT7925_PATCH_MCU_1_1_hdr.bin.zst "
install_items+=" /usr/lib/firmware/mediatek/mt7925/WIFI_RAM_CODE_MT7925_1_1.bin.zst "
```

