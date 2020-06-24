---
title: "Using Nextflow's Map, Flatten, and Collate"
excerpt: "Iterate over channel object list to create new channel objects"
tags: Nextflow Groovy
---

### The Issue
I recently ran into a problem where I wanted to create multiple narrowPeak files using just one BAM file. Creating these narrowPeak files was easy enough (Bash for loop), but later in the pipeline I calculate the coverage of each base in my narrowPeak file. This requires one narrowPeak file with its respective BAM file. I previously put them into the same channel which worked fine; however, creating multiple peak files at the same time from the one BAM file and putting them all into the same channel didn't work. Rather than put each peak file into its own channel (which would be way more channels than I would want to create), I used this opportunity to learn more about Nextflow and Groovy syntax.

I first collect all my narrowPeak files into one channel and my bam files into another channel.

```
set val(name), file("*.narrowPeak") into ch_narrowPeaks
file(bam_files) into ch_bam
```

Then I merge these two channels (outside of a process) into one channel for calculating per-base coverage.

```
ch_narrowPeaks .merge(ch_bam)
               .set{ ch_pbc }
```

This next part is what took me a while to figure out. Currently, the output of our `ch_pbc` has the format of [name, narrowPeak(s), bam, bam.bai]. If the narrowPeaks part of the output is the list, how can I create a new output with each narrowPeak file with the same BAM?
### The solution
```
ch_pbc .map { it -> [it[1],[it[2]]].combinations() }
       .flatten()
       .collate( 2 )
       .set{ ch_pbc }
```
### How it works
That's all it took! Now let's walk through what this is doing. First, we are going to change, or "map", our output so we only have the combinations of the narrowPeaks and Bams (removing the name and bam index). The `combinations()` function gives all the different combinations of everything within the square brackets. Because the BAM file wasn't originally in an array like the list of narrowPeaks, I have wrapped it in square brackets. This mapping results in a list of lists which isn't usable. Thus, we `flatten` all the values into one list (the values maintain their order). Then we use `collate`, which will create new objects, each with the length passed in as the parameter. We've finally formatted correctly, so let's `set` this channel back to the original channel name. Below is an example of what the channel looks like at each state.
```
ch_pbc -> ['sample1', ['sample1-q1.narrowPeak', 'sample1-q2.narrowPeak'], 'sample1.bam', 'sample1.bam.bai']
ch_pbc.map -> [['sample1-q1.narrowPeak', 'sample1.bam'], ['sample1-q2.narrowPeak', 'sample1.bam']]
      .flatten -> ['sample1-q1.narrowPeak', 'sample1.bam', 'sample1-q2.narrowPeak', 'sample1.bam']
      .collate -> ['sample1-q1.narrowPeak', 'sample1.bam']
                  ['sample1-q2.narrowPeak', 'sample1.bam'] 
```
And that is how you can iterate over a list in a channel to create new channel objects!
