# LinuxBIOS--Libreboot
precarious delicate 
Copyright (c) 2026 Christopher T. Williams
License

Permission is granted to use, copy, modify, and distribute this software solely for non-commercial research, testing, and security-analysis purposes, provided that the copyright notice and this permission notice are retained.

Commercial use, sale, marketplace distribution, or monetization of this software, in whole or in part, is strictly prohibited without prior written consent from the author.

THIS SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. THE AUTHOR SHALL NOT BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY ARISING FROM THE USE OR OTHER DEALINGS IN THE SOFTWARE.

https://www.amazon.com/dp/B0DC9Q7BC8?ref=ppx_yo2ov_dt_b_fed_asin_title

#inject libbre from source folder

curl -fL --retry 3 \
  -o /data/sda4/libre/libreboot-26.10_hp2560p_8mb.tar.xz \
  https://mirror.math.princeton.edu/pub/libreboot/stable/26.10/roms/libreboot-26.10_hp2560p_8mb.tar.xz

  
curl -fL --retry 3 -o /data/sda4/libre/libreboot-26.10_src.tar.xz https://mirror.math.princeton.edu/pub/libreboot/stable/26.10/libreboot-26.10_src.tar.xz


tar -xJf /data/sda4/libre/libreboot-26.10_src.tar.xz -C /data/sda4/libre


cd /data/sda4/libre/libreboot-26.10_src


runuser -u linuxuser -- ./mk inject /data/sda4/libre/libreboot-26.10_hp2560p_8mb.tar.xz


#flash to chip

/data/flashprog-private/bin/flashprog -p ch341a_spi -c "W25Q64BV/W25Q64CV/W25Q64FV" -w /data/sda4/libreboot-ready/bin/hp2560p_8mb/edk2_grub_seabios_hp2560p_8mb_libgfxinit_corebootfb.rom
#inspect

/data/flashprog-private/bin/flashprog -p ch341a_spi -c "W25Q64BV/W25Q64CV/W25Q64FV" -v /data/sda4/libreboot-ready/bin/hp2560p_8mb/edk2_grub_seabios_hp2560p_8mb_libgfxinit_corebootfb.rom
