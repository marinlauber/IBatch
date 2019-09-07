# IBatch

Hold various batch scripts to run different programs on Iridis 4. 


## Iridis 4 useful commands:

To query the size of a certain directory, use the command

```
  du -h dir/
```

which return disk usage (```du```) in a human-readable format (```-h```) of the particular directory. A standard input would be
```
$ du -h dir/
  32K	dir/datp
  232M	dir/dat3x3x0
  405M	dir/dat1x1x0
  260M	dir/dat3x2x0
  406M	dir/dat2x1x0
  260M	dir/dat3x1x0
  318M	dir/dat0x2x0
  319M	dir/dat2x0x0
  319M	dir/dat0x1x0
  406M	dir/dat2x2x0
  291M	dir/dat0x3x0
  232M	dir/dat3x0x0
  318M	dir/dat2x3x0
  403M	dir/dat1x2x0
  319M	dir/dat1x3x0
  260M	dir/dat0x0x0
  318M	dir/dat1x0x0
  95M	  dir/render
  5.1G	dir/
$
```
