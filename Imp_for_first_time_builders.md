# If you started building TWRP/ROM then these instructions are for you.

After **repo initialization and before repo sync** you have to add a file for syncing device tree and kernel source (for TWRP). In case of ROM you have to add vendor tree also.


A. __Instructions (after repo init):__

1. ```cd <source_dir>``` **Here source directory means location of TWRP/ROM source code**

2. ```cd .repo/```

3. ```mkdir local_manifests;```

4. ```cd local_manifests;```

5. ```nano roomservice.xml```

Now a file has been created and you have include various trees for building. 

roomservice.xml will be like this.

```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

<project name="buddi56/android_device_oppo_CPH1859" path="device/oppo/CHP1859" remote="github" revision="CPH1859_Android_9" />
###<project name="buddi56/android_kernel_oppo_CPH1859" path="kernel/oppo/CPH1859" remote="github" revision="master" />###

</manifest>
```

Kernel source is available but it has lot of issues, so used prebuilt kernel. 

**Note:** Using prebuilt kernels in building is deprecated.

Now perform 

    repo sync -j(nproc --all) -c

All the sources along with your TWRP device tree and kernel (if available) will be downloaded.



B. __Instructions (After repo sync):__

After repo sync you have to tell buildbot to include your device for building TWRP. So for this you can either make a **vendorsetup.sh** file in your device tree or can edit an available file in TWRP source.

To edit vendorsetup.sh file in the downloaded source. Head to the below location.

1. ```cd <source_dir>/vendor/omni/```

2. ```nano vendorsetup.sh```

Now add below line at the end.

    add_lunch_combo omni_CPH1859-eng

3. Save file and exit.

You can also choose user or userdbug. But eng build is best for a custom recovery.


**Now start the compilation using the command given in README.md**
