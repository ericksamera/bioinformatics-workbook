---
description: >-
  From Nobel Prize-winning technique to undergraduate exercise: A review of
  Sanger sequencing.
---

# Review of Sanger Sequencing

{% hint style="info" %}
**Learning Objectives**

* [ ] Understand the principles and technology behind Sanger sequencing, including DNA replication and dideoxynucleotide termination.
* [ ] Recall the steps of performing Sanger sequencing in the laboratory, including PCR amplification, and sequencing reaction preparation.
* [ ] Understand the output of Sanger sequencing: the chromatograms, the basecalls, and how to analyze and interpret the results.
  * [ ] Recognize and troubleshoot common issues in electropherogram data.&#x20;
* [ ] Appreciate the wet-lab preparation required in data analysis and the importance of understanding the sample input to receive the data output.
{% endhint %}

## Background

Before we discuss the analysis of data from Sanger sequencing — or any data, for that matter — it's important to know how the data came to be. This section will provide a brief review of Sanger sequencing (which you've hopefully already heard from Lyndsey). If you're already comfortable with this, I'd skip ahead to the AplasmidEditor section.

Sanger sequencing, also known as the [chain termination method](#user-content-fn-1)[^1], is a classic DNA sequencing technique that revolutionized the field of molecular biology. This method is based on the principle of DNA replication and utilizes modified nucleotides to terminate the growing chain of DNA, resulting in a series of fragments of varying lengths that can be used to deduce the sequence of the original DNA molecule. Sanger sequencing has been instrumental in numerous scientific breakthroughs and is still used today (especially in our lab) for various applications, such as mutation detection, identification, and verification of recombination.

### DNA replication

DNA replication is the process by which a cell makes an identical copy of its DNA. This is a crucial step in cell division and ensures that each new cell receives a complete set of genetic information. In DNA replication, the double-helix is locally unwound so that DNA polymerase is able to bind to single-stranded primers and incorporate nucleotides to the new strand using a template strand. This biological replication system is taken advantage of in PCR and Sanger sequencing to make multiple copies of our target sequence.&#x20;

### Dideoxynucleotide termination

Usually when you use DNA polymerase for PCR, it will incorporate dNTPs using phosphodiester bonds until  it reaches the end of the strand. With Sanger sequencing, in addition to regular nucleotides (dNTP), we also give polymerase a set of dideoxynucleotides (ddNTP). The dideoxy- characteristic makes it so that when DNA polymerase attaches it to the nascent strand, [it is unable to attach any more](#user-content-fn-2)[^2].&#x20;

Consider this strand of DNA:

```
CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAACTCTCAGATAGT
```

We give DNA polymerase its cocktail of dATP and ddATP, along with regular dTTP, dCTP, and dGTP. By random chance of picking dATP it will be able to extend the chain. By random chance of picking ddATP instead, the chain will stop and it cannot extend it any further.

<pre data-title="Sanger fragments (ddATP)"><code>CCTA*
CCTATGCA*
CCTATGCACTTTGTACA*
CCTATGCACTTTGTACAGGGTGCCA*
CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGA*
CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAA*
CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAACTCTCA*
<strong>CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAACTCTCAGA*
</strong>CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAACTCTCAGATA*
CCTATGCACTTTGTACAGGGTGCCATCGGGTTTCTGAACTCTCAGATAGT
</code></pre>

And we can do the same thing for ddTTP, ddCTP, and ddGTP.

Now the we have _differently-lengthed_ fragments of DNA, we can figure out where ddNTP was added if we know [the length of DNA](#user-content-fn-3)[^3].

{% hint style="info" %}
Put all the pieces together. Consider how that might look on a gel with running differently-sized fragments of DNA, depending on the nucleotide that was added.
{% endhint %}

Old-school Sanger sequencing was run on a gel with separate lanes for each dideoxynucleotide to determine nucleotide sequence (pictured below).

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuXQehO6lArpiroG7tIdI%2Fuploads%2FALCL2cUT2EdiEP2CjuT7%2Fimage.png?alt=media&#x26;token=3564065d-7eaa-4263-ab49-99dfccb32dc7" alt=""><figcaption><p><strong>Figure 1.</strong> Old-school Sanger with a gel.</p></figcaption></figure>

## Sanger sequencing in the lab

Almost 50 years later, the idea for Sanger sequencing hasn't changed too much. But, of course, there are some slight differences to make things easier and more efficient:

* We use fluorescently-labeled dideoxynucleotides so that we can use fluorescence and detectors to "read" the nucleotides as the move.
* We still use a gel, but it's a capillary-based gel now.
* We don't really need to load the gel ourselves. There's a liquid-handling machine that deals with pipetting the Sanger fragments and runs the gel.
* A little quirk with our machine, but it loads samples in groups of 4.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuXQehO6lArpiroG7tIdI%2Fuploads%2FY8nnu2YzHkEKN7ASSVdE%2Fimage.png?alt=media&#x26;token=53fbfae4-fcc5-4667-ba3c-f9849d1777fa" alt=""><figcaption><p><strong>Figure 2.</strong> Summary graphic of how modern Sanger sequencing is performed at our lab.</p></figcaption></figure>

Overall, it takes about an hour or so to sequence 600 bp which is pretty fast! The [slow step](#user-content-fn-4)[^4] is the amount of time it takes to prepare samples for Sanger sequencing. After PCR and visualization (to verify amplification), there is a round of cleanup, quantification, amplification again, another cleanup, then extraction before loading samples into the sequencer. For even an experienced technician, this is still at least a half-day for one run.

{% hint style="info" %}
If you have it, maybe take a look through the lab manual and review the protocol for Sanger sequencing. Compare this with regular PCR and consider the differences which make Sanger sequencing possible.
{% endhint %}

## The electropherogram/chromatogram

Because modern Sanger sequencing uses a system of fluorescence and detectors to track the migration of fragments over time, our data at the end is not a gel image, but a fluorescence-time[^5] graph.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FuXQehO6lArpiroG7tIdI%2Fuploads%2FLYDfFGhx9oRkiwWquW9h%2Fimage.png?alt=media&#x26;token=10fd9410-27f1-4232-84c7-28db845619c8" alt=""><figcaption><p><strong>Figure 3.</strong> Modern techniques in Sanger sequencing with capillary electrophoresis and fluorescence is not that much different from old-school Sanger. The concepts carry over pretty straight-forwardly.</p></figcaption></figure>

When reading the [data from a Sanger sequencing run](#user-content-fn-6)[^6], all the information comes from these peaks of fluorescence. The **colour** of the peak tells us which nitrogen base was detected. The **migration time** tells us where that nucleotide is in the amplicon we're sequencing.

{% hint style="info" %}
Sanger sequencing reads nucleotides per base position. Can you think of a scenario where Sanger might read 2 different nucleotides at the same base position?
{% endhint %}

## Summary

Sanger sequencing is performed at our lab for genotyping and species identification. It uses the chain-termination method with dideoxynucleotides to create Sanger fragments. Old-school Sanger sequencing used gel electrophoresis to identify the sequence, but modern Sanger sequencing now uses capillary electrophoresis with fluorescent dideoxynucleotides

The data produced from Sanger sequencing is an electropherogram which contains peak data. The electropherogram can tell a lot about the quality of the sequence.

[^1]: They really should change its name to this. This is much more descriptive of how the sequencing works.

[^2]: This is where the chain-termination comes in.

[^3]: **Hint hint:** it is our favourite molecular biology technique: gel electrophoresis.

[^4]: Read: absolutely rate-limiting

[^5]: We can correlate the migration time to basecall positions, so really it's more fluorescence over positions of nucleotides.

[^6]: This is the electropherogram, or sometimes called the chromatogram.
