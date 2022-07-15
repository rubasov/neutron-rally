This repository contains Rally reports exercising the Neutron API for 10
consecutive OpenStack releases: Pike through Yoga.  The purpose was to get
some sense of how the Neutron API performance changed in the recent past.

Original email sent to openstack-discuss@lists.openstack.org:

http://lists.openstack.org/pipermail/openstack-discuss/2022-July/029384.html

The test setup for all Rally runs were the same.  Rally was running
directly on a Linux laptop in a virtualenv. Each Rally task was executed
3 times.

An all-in-one devstack was running in a libvirt/kvm VM on the same laptop.
Devstack was built with the same local.conf except what must have been
changed like TARGET_BRANCH.

In devstack a single neutron-server was running.  Neutron was configured
to use the ml2/ovs backend. While testing with other backends like ml2/ovn
would also be interesting, first I wanted to create measurements that
are directly comparable.

The contents of this tarball are:

* readme.txt (this file)

  Notes on how to interpret and reproduce these test results.

* versions.txt

  All relevant software versions used in these test runs.

* input/
  input/local.conf
  input/rally.conf
  input/task-neutron.yaml

  Configs used in creating the test environment like
  devstack's local.conf.  And the Rally task file (taken
  from openstack/neutron/rally-jobs/task-neutron.yaml).

* reports/
  reports/pike/1/output.html
  ...
  reports/yoga/3/output.json

  The Rally reports saved in .html and .json formats organized in folders
  by OpenStack version and Rally run count.

* tools/
  tools/plot-rally-csv
  tools/rally-reports-to-csv

  Two trivial scripts to plot the single most important metric
  (load_duration) of each Rally scenario by OpenStack version.

* charts/load_duration.png

  Plot of Rally scenario load_durations by OpenStack version. The
  load_durations for the 3 repeated runs were averaged.

## Details of the test environment

devstack (libvirt/kvm) vm
ram: 6 GiB
vcpu count: 2

hw of hypervisor (laptop)
laptop model: Lenovo ThinkPad T480
cpu: Intel(R) Core(TM) i7-8650U CPU @ 1.90GHz
disk: SAMSUNG MZVLB512HBJQ-000L7 (NVMe)

cpu flags
hypervisor: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust sgx bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d
guest: fpu de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 syscall nx lm constant_tsc nopl xtopology cpuid tsc_known_freq pni cx16 x2apic hypervisor lahf_lm cpuid_fault pti

## Credits

Author: Bence Romsics (rubasov) <bence.romsics@est.tech>
License: https://creativecommons.org/licenses/by/4.0/
Date: 2022w26
