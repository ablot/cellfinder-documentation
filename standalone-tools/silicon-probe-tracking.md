---
description: >-
  Analysis of silicon probe tracks (e.g. Neuropixels) in brains imaged post-hoc
  in a standard coordinate space
---

# Silicon probe tracking

{% embed url="https://youtu.be/0-sM-desUmE" caption="Probe track tracing video" %}

### Introduction

The aim of electrophysiological recordings using silicon probes is to record neuronal activity across brain regions and animals. It is therefore fundamental to record precisely the localisation of the probe \(or multiple probes\) in each brain and be able to compare probes across animals.

Here we describe a tool for the analysis of silicon probe tracks \(e.g. [Neuropixels](https://www.neuropixels.org/)\) in brains imaged post-hoc in a standard coordinate space. This tool is packaged as part of the cellfinder suite of tools for whole-brain microscopy image analysis.

###  **Before tracing probe tracks**

In order to label the probe penetration track in the brain, the probe is delicately coated with DiI \(Molecular Probes, Cat\# V22885\) using a pipette tip \(**Fig. 1**, left\). The probe is then attached to a micromanipulator and the probe tip lowered to touch the surface of the brain \(e.g. in head-fixed mice\). This position is recorded as position “zero”. The probe is then introduced in the brain at a speed of ~10μm per second to the desired penetration depth \(in our case 1750μm; **Fig. 1**, centre\). 

![Figure 1.](../.gitbook/assets/fig1.png)

{% hint style="info" %}
The final penetration depth has to be recorded precisely \(e.g. with the micromanipulator readout\) in order to know how much of the probe shank was used to record neuronal activity. This will allow to compare traced probe tracks and electrophysiological data.
{% endhint %}

When the experiment is done and the probe is retracted, the animal is anaesthetised and perfused with PFA 4% following standard perfusion protocols. The brain is carefully extracted and left in PFA 4% overnight.

{% hint style="info" %}
 To ensure high quality image registration, it is essential that the brain is properly perfused in order to decrease the autofluorescence of blood vessels. It is also important that the brain is extracted from the skull carefully in order to avoid tissue damage.
{% endhint %}

The brain is then thoroughly washed with 100mM PBS and imaged \(e.g. by [Serial 2-Photon Tomography](https://sainsburywellcomecentre.github.io/OpenSerialSection/acquisition/#); **Fig. 1**, right\). We imaged 2 channels \(one where DiI signal is detected and one with background fluorescence only\) at a resolution of x = 5μm, y = 5μm, z = 20μm.

{% hint style="info" %}
 It is important to image both the DiI probe signal and the brain’s background fluorescence in two independent channels. The background signal will be used to register the brain into standard space \(since the probe signal might interfere with the quality of registration\).
{% endhint %}

### **Brain registration to an atlas**

To track the probe in standard space, the brain must first be registered to an atlas using amap.

Before registration, cellfinder \(which includes amap\) needs to be installed. Please follow the instructions [here](../installation/installation.md). Once cellfinder is installed, we can proceed to register the imaged brain.

{% hint style="info" %}
Make sure you activate your conda environment before starting
{% endhint %}

You will need:

1. The path where the brain image stack \(DiI signal channel\) is located
2. The path where the brain stack \(background fluorescence channel\) is located. 
3.  The path where you want the registration result to be saved
4. The resolution at which the brain was imaged

**To register your brain to an atlas, please follow the instructions for amap** [**here**](../amap/getting-started/)**.**

An example registration command is as follows:

```text
 amap /path/to/signal/channel1.tiff /path/to/output/directory -x 5 -y 5 -z 20 /path/to/background/channel2.tiff
```

 A new output directory has been created, which contains the registered brain. We are now ready to manually trace the probe track.

###  **Probe track tracing**

{% hint style="warning" %}
Make sure your conda environment is still activated!
{% endhint %}

 To open the graphical user interface, type the following command:

```text
manual_seg
```

 The `manual_seg`graphical user interface opens and shows a set of tools. A detailed description of these tools can be found in the legend of **Fig 2**. For a step-by-step description of how to manually trace a probe track with cellfinder, please see the video at the top of this page. There is also some more information at the main page for this tool, [here](../neuro/standalone-tools/manual-segmentation.md).

{% hint style="info" %}
When tracing the probe track, add the markers in the order you wish them to be connected. You can also add a marker that is exactly at the surface of the brain by ticking the box “add surface point” \(**Fig. 2b**\).
{% endhint %}

![Figure 2.](../.gitbook/assets/fig2.png)

### Figure 2:

**a. The layers tool box**. At the bottom can be found the layers shown in the central screen. In this case, only one layer is present, called `Image in standard space`, highlighted in blue. At the top are a set of tools that affect the layer highlighted. In this case, the layer highlighted called `Image in standard space` is the brain image stack, therefore the tools available allow to adjust the visualisation of the image stack.

**b. The project tool box**. Here, the image stack can be loaded \(`Load project`\). An atlas can be overlaid to the brain stack \(`Load atlas`\). A probe track tracing can be added \(`Add track`\). Finally, track markers \(also called points\) can be fitted \(`Trace tracks`\). The fitting properties can be adjusted by fit degrees, spline smoothing and spline points \(i.e. the number of points used to sample the fit\). A marker at the exact position of the surface can be added by ticking the `Add surface point` box.

**c. The brainrender tool box.** The manually traced probe tracks can be previewed in [brainrender](https://github.com/BrancoLab/BrainRender). In addition to probe tracks, one brain region can be visualised by choosing it in the drop-down list `Region to render`. The transparency of the region to render can be adjusted with `Atlas region alpha`. The probe track can be saved in the registration directory, under `manual_segmentation/tracks/name_of_track.h5` and `manual_segmentation/tracks/name_of_track.csv`. The `name_of_track.csv` file shows the localisation of the probe track following standard brain atlas region annotations.

{% hint style="info" %}
This user interface is built upon [napari](https://napari.org/). For more information about navigating your data in this viewer, please see the [napari tutorial](https://napari.org/tutorials/fundamentals/viewer).
{% endhint %}

{% hint style="info" %}
If you have any questions about manually tracing probe tracks, please raise them on the forum [here](https://gitter.im/cellfinder/probe-tracking). For general cellfinder questions please ask in the appropriate channel [here](https://gitter.im/cellfinder/).
{% endhint %}

**By** [**Mateo Vélez-Fort**](https://www.sainsburywellcome.org/web/people/mateo-velez-fort)\*\*\*\*



