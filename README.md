# HP800G1TWR-OC-BigSur11.2.3

wrote : 25 May 2021, doogiejoe

### Worked and include
- HP 800 G1 Tower (BIOS(L01), Ver: 02.78 Rev.A, Apr 29, 2020)
- i7-4770 CPU @ 3.4GHz, 32GB 1600MHz DDR3 memory
- Graphics HP GeForce GT 630 2048MB
- (Added) RTL8111/8168/8411 Ethernet NIC
- (Disks) SSD 250GB *2, 2TB HDD
- (BT) inote BCM VPULSE BT Dongle
- All General macOS Features
  - BT, Sleep/Wake, AirDrop, iCloud
 
### Not include or More Things you can
- Opencore GUI Boot
- Headless with iGPU
- iMessage (im not use)
- Big Sur USB3.0 Trouble & USBPort Map (at over BigSur 11.3)

### guide: BIOS Setup
- start with Factory Default BIOS setup 
- Security > Network Boot > Disable
- Security > Master Boot Record > Disable
- Security > System Security
    - Data Execution Prevention : Enable
    - VTx : Enable
    - VTd : Disable
    - Embeded Security Device : Disable (Need setup passwd, therefore, im Enabled)
    - OS management of Embedded Security Device : Enable
- Security > Secure Boot Configuration
    - Legacy Support : Disable
    - Secure Boot : Disable
    - Key Management > Dont Clear & HP Keys
    - Fast Boot : Disable
- Poewr > OS Power Management
    - Runtime Power Management : Enable
    - Idle Power Savings : Extended
    - Unique Sleep Status Blink Rates : Disabled
- Power > Hardware Power Management
    - SATA Power Mangement : Enable
    - PCI Express Power Management : Enabled
    - S5 Mazimum Poewr Savings : Disable
- Advanced > Power-On Options
    - POST Mode : Quick Boot
    - POST Message : Enable
    - Press the ESC key for Startup Menu : Enable
    - Option ROM Prompt : Enable
    - After Power Loss : Off
    - POST Delay : None
    - Remote Wakeup Boot Source : Local Hard Drive
    - Factory Recovery Boot Support : Disable
    - Bypass F1 Prompt on configuratino Changes : Disable
    - POST Memory manager Runtine Allocation : Disable
- Advanced > Onboard Device > Disable
- Advanced > BUS options
    - PCI SERR# Generation : Enable
    - PCI VGA Palette Snooping : Disable
- Advanced > Device Options
    - Turbo Mode : Enable
    - Integrated Video : Enable
    - Internal Speaker : Enable
    - USB EHCI Port Debug : Disable
    - USB3.0 BIOS Driver Support : Disable
    - Multi-Processor : Enable
    - Hyperthreading : Enable
- Advanced > VGA Configuration > Nvidia VGA controller : Primary VGA device
- Advanced > Management Operations
    - AMT : Enabled
    - Unconfigure AMT/ME : Disable
    - Hide Un-Configure ME confirmation prompt : Disable
    - WatchDog Timer : Disable
- Advanced > Option ROM Launch Policy (IMPORTANT)
    - PXE Option ROMs : UEFI Only
    - Storage Option ROMs : UEFI Only
- Advnaced > Connected BIOS : Disable

### guide: make EFI
- Generally, follow Dortania Guide & bellows
   - system Type : iMac15,1
   - DeviceProperties : PciRoot(0x0)/Pci(0x2,0x0) for iGPU : 
      - AAPL,ig-platform-id : 0300220D (data)
      - device-id : 12040000 (data)
   - DeviceProperties : PciRoot(0x0)/Pci(0x2,0x0) for audio :
      - layout-id : 0B000000 (data, work afeter HPET patch)
- added Patch about HPET for  ALC221
   - need SSDT-HPET.aml and relative ACPI Patch (HPET CSR, RTC IRQ 8, TIMER IRQ 0)
   - you make SSDT patch file on Windows with SSDTTime OR get SSDT-HPET.aml from internet
   - and inject SSDT-HPET.aml to EFI/OC/ACPI and patch Values for Patch of ACPI to config.plist

FIN.

