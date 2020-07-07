---
description: Downloading the files that cellfinder needs
---

# Downloading files

## Download atlas and trained classification models \(optional\)

When cellfinder runs, the appropriate machine learning models and reference atlas will be downloaded \(if not previously done so\). If you would like to download in advance to save time \(or if you will not have an internet connection\) please use `cellfinder_download`.

Currently, the only supported atlas is the Allen reference mouse brain, originally from [here](http://help.brain-map.org/display/mouseconnectivity/API#API-DownloadAtlas). The atlas will download into `./cellfinder/atlas`.

In the future, other atlases will be available, and you will be able to choose which is downloaded.

If you want to modify the cellfinder download, use:

* `--install-path` Supply a path to download the atlas elsewhere. This 

  should also update the default `cellfinder.conf` file so that the correct 

  atlas is sourced. Alternatively, use this command to tell cellfinder where an 

  existing atlas is, to save it being downloaded twice. \(Requires 20GB 

  disk space\)

* `--download-path` The path to download the atlas into. 

  \(Requires 1.2GB disk space\). Defaults to `/tmp`.

