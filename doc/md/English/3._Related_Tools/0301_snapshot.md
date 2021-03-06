# Snapshot data handling

## `read_snp.x` 

Snapshot files in both `NetCDF` and the originally defined binary format
can be extracted or visualized by the program `read_snp.x`.


``` bash
read_snp.x -i snapshotfile [-h] [-ppm|-bmp] [-pall] 
              [-mul var | -mul1 var -mul2 var ...] [-bin] [-asc] [-skip n]
```

  `-h`
  : Print the header information defined in the snapshot, as in the
    following example.

    ``` txt
     $ ../bin/read_snp.x -i swpc_3d.xz.ps.snp -h

     [binary type]   : STREAMIO
     [code type]     : SWPC_3D
     [header version]:          3
     [title]         : swpc_3d
     [date generated]: 1408015126
                       2014-08-14T11-18-46
     [coordinate]    : xz
     [data type]     : ps
     [ns1]           :        256
     [ns2]           :        256
     [beg1]          :       -63.87500
     [beg2]          :        -9.87500
     [ds1]           :         0.25000
     [ds2]           :         0.25000
     [dt]            :         0.05000
     [na1]           :         20
     [na2]           :         20
     [nmed]          :          3
     [nsnp]          :          2
     [clon]          :       143.50000
     [clat]          :        42.00000
    ```

  `-ppm`, `-bmp`
  : Visualize and export the image files in ppm or bmp format. The `ppm`
    or `bmp` directory will be automatically created in the current
    directory and image files with sequential numbers will be stored
    there. If the snapshot file is displacement or velocity, the
    absolute values of the vertical and horizontal amplitudes will be
    colored red and green, respectively. For the `PS` file, the absolute
    values of the divergence and rotation vector will be colored
    similarly. If the absolute value option is specified, the
    black-red-yellow-white color palette (similar to the "hot" color
    palette in GMT) will be adopted. For cross sections along the
    surface (`ob`, `fs`), the topography color map will be overlaid. For
    other cross sections, the velocity structure in the section will be
    overlaid.

!!! bug "Limitation of the BMP format"
    Output to `bmp` format occasionally fails as this format has a restriction to the image size. `ppm` format is recommended. 
      
  `-pall`
  : Visualize including the absorbing boundary region. This option works
    only if it is used with . By default, the absorbing boundary region
    will be clipped.

  `-mul`
  : Multiply `var` by the amplitude for visualization. Adjust the
    visualized color by changing this value. Optionally, by specifying
    `-mul1` or `-mul2`, for example, one may change the weight of the
    amplitude by component.

  `-abs`
  : Visualize the absolute value of the vector. This only works with the
    velocity or displacement snapshots.

  `-bin`, `-asc`
  : Export the snapshot data to binary (`-bin`) or ascii (`-asc`) files.
    The data file will be created in the automatically created `bin` or
    `asc` directories. The binary formatted data can be directly used in
    `GMT` with the `xyz2grd` module by appending the `-bis` option.

  `-skip n`
  : Skip the first $n$ snapshots for visualization or data exports.

## `diff_snp.x`

This program takes the difference between two snapshots and exports it
to another snapshot file.

``` bash
$ diff_snp.x snap1 snap2 diffile
```

The output file format (`NetCDF` or binary) depends on the input file
format.
