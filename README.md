# Stitch

Austin Glenn Davis-Richardson
<harekrishna@gmail.com>

Working under Dr. Eric Triplett & Dr. Adriana Giongo

## Description:

Illumina sequencing has the ability to generate "paired ends."
We did an experiment where our paired ends overlapped.
I wrote this script to assemble these overlapping paired ends into contigs.

It does a simple alignment.  Finding the best possible overlap.  The simple
alignment does not take into account gaps which are uncommon.  This was done
for simplicity and speed.

### Score Calculation:

Scores are calculated with the following equation:

`matches - mismatches / (length-of-overlap)`

The default is 0.6 meaning that 60% of the bases in the overlap matched.
Stitch calculates all possible overlaps and chooses the one with
the highest score.  Matches of `N` to `N` are not counted.

### Pipelineing

* Importing from Python:

		from stitch import *
		stitch(options={
	  	'filea': 'filenamea',
	  	'fileb': 'filenameb',
	  	'prefix': 'data/stitched.fastq',
	  	'pretty': False,
	  	'threads': None,
	  	'score': None })
		
* You could also just use `subprocess.Popen`:

		from subprocess import Popen
		Popen.(['stitch','-i','filea','-j','fileb','-o','output'])

* Or from Ruby/Perl:

		system('stitch -i filea -j fileb -o output')
    
		
## Installation

1. Once in the stitch directory do:
   > `$ sudo python setup.py install`

2. Stitch should have installed successfully meaning that you can now do this:
   > `$ stitch -h`
   to display help information

## Usage

Do this:

> `$ stitch -i <fastq file 1> -j <fastq file 2> -o <output prefix>`

Where `fastqfile1` is the 5' most and `fastqfile2` is the 3' most.

Other options:

 - `-h` prints help
 - `-t [THREADS]` specify number of cores to use (Default=all)
 - `-s [SCORE]` minimum score (Default=0.6)
 - `-p pretty output` prints a user-friendly output.  Useful for adjusting
   score.

## Bugs

 - Don't know of any at the moment
   if you find one, [let me know]!(https://github.com/audy/stitch/issues) thx.

## Features

 - Automatically joines overlapping paired ends!
 - **Multithreaded** - Automatically uses all cores on your system!
 - Generates 3 files: `contigs`, duds from `fastqfile1` and duds from
   `fastqfile2`

## Know your rights

Stitch is free and open-source.
See LICENSE (GNU GPL v3)