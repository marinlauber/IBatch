# IBatch

Hold various batch scripts to run different programs on Iridis 4. 


## Iridis 4 useful commands:

Copy file from local machine to Iridis login nodes (logged-in local machine)

```
  scp file username@iridis4_a.soton.ac.uk:~/Dir
```

or from Iridis to local machine (at current location):

```
  scp -r username@iridis4_a.soton.ac.uk:~/Dir .
```

Send a batch job on the queue:

```
  qsub subLotus
```

Query status of jobs:

```
  qstat
```

Can also use the ```watch``` comman, which refreshes the command every 2 seconds.

Look at the queue (running only):

```
  showq -r
```

Show user queue:

```
  showq -u userID
```

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

Generate video from a collection of images, using ```ffmpeg```. Assuming a list of pic0001.png, pic0002.png, ..., pic%04d.png that we want to transform in a video called test.mp4. Can adjust the frame rate (```-r fps```)

```
  ffmpeg -r 30 -f image2 -s 1920x1080 -i pic%04d.png -vcodec libx264 -crf 25 -pix_fmt yuv420p test.mp4
```
