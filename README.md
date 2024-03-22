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
  qsub subLotus (or pyrun, etc.)
```

Query status of jobs:

```
  qstat
```

Can also use the ```watch``` command, which refreshes the command every 2 seconds.

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

which returns disk usage (```du```) in a human-readable format (```-h```) of the particular directory. A standard input would be
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
  95M	dir/render
  5.1G	dir/
$
```

Show user quota in the home and scratch folder on Iridis 4
```
  mmlsquota --block-size=G home scratch
 ```

Generate video from a collection of images using ```ffmpeg```. Assuming a list of pic0001.png, pic0002.png, ..., pic%04d.png that we want to transform in a video called test.mp4. Can adjust the frame rate (```-r fps```)

```
  ffmpeg -r 30 -f image2 -s 1920x1080 -i pic%04d.png -vcodec libx264 -crf 25 -pix_fmt yuv420p test.mp4
```
To make a `gif` from this `mp4` file, use
```
ffmpeg -i input.mp4 -vf "fps=16,scale=160:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=32:reserve_transparent=0[p];[s1][p]paletteuse" -loop 0 output.gif
```
where we have limited the number of colors used to save space.
```
ffmpeg -i %06d.png -vf "fps=10,scale=-1:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=32:reserve_transparent=0[p];[s1][p]paletteuse" -loop 0 falling_fillament.gif
```

## Saving Figures from matplotlib

In order to be able to generate figures using matplotlib in Iridis4, we need to specify the AGG backend. Otherwise, matplotlib will look for a `$DISPLAY` to show the figure. This is done as follows
```
  import matplotlib
  matplotlib.use('Agg')
  import matplotlib.pyplot as plt
```
Which must be placed on the first line of your `main.py` file.

## Ansys CFX Batch

Ansys CFX uses `ssh` to communicate between nodes by default, for this the ssh connections need to be made without having to enter a password. To create `ssh` keys to connect to internal cluster nodes you have to:

1. Generate the keys
```
  sss-keygen
```
2. add the generated keys to the list of authorized keys
```
cd ~/.ssh && cat id_rsa.pub >> authorized_keys
```
This will the allow you to run the `qsub run_cfx` script.
