# ubuntu22.04 笔记本自带键盘开启与关闭

## 查看所有设备
```
xinput list
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=19	[slave  pointer  (2)]
⎜   ↳ USB OPTICAL MOUSE  Keyboard             	id=16	[slave  pointer  (2)]
⎜   ↳ USB OPTICAL MOUSE                       	id=23	[slave  pointer  (2)]
⎜   ↳ SINO WEALTH Wired Gaming Keyboard Consumer Control	id=10	[slave  pointer  (2)]
⎜   ↳ SINO WEALTH Wired Gaming Keyboard Mouse 	id=15	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Power Button                            	id=9	[slave  keyboard (3)]
    ↳ HP Wide Vision HD Camera: HP Wi         	id=17	[slave  keyboard (3)]
    ↳ Wireless hotkeys                        	id=20	[slave  keyboard (3)]
    ↳ HP WMI hotkeys                          	id=21	[slave  keyboard (3)]
    ↳ USB OPTICAL MOUSE  Keyboard             	id=22	[slave  keyboard (3)]
    ↳ SINO WEALTH Wired Gaming Keyboard Consumer Control	id=11	[slave  keyboard (3)]
    ↳ SINO WEALTH Wired Gaming Keyboard System Control	id=12	[slave  keyboard (3)]
    ↳ SINO WEALTH Wired Gaming Keyboard       	id=13	[slave  keyboard (3)]
    ↳ SINO WEALTH Wired Gaming Keyboard       	id=14	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=18	[slave  keyboard (3)]
```
## 关闭键盘
```
xinput set-prop 18 "Device Enabled" 0
```

## 开启键盘
```
xinput set-prop 18 "Device Enabled" 1
```