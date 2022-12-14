# jasmr
jasmr directory of translations for DLSite voice works.

## Archive Structure
---
```
π¦example
 β£βββπartwork  [ππ³π΅πΈπ°π³π¬ π§πͺπ­π¦π΄]
 β£βββπdeepld   [ππ³π’π―π΄π­π’π΅π¦π₯ π£πΊ ππ¦π¦π±π]
 β   β£βββπlrc
 β   β   β£βββπpart1
 β   β   ββββπpart2
 β   ββββπsrt
 β£βββπoriginal [ππ³πͺπ¨πͺπ―π’π­ π§πͺπ­π¦π΄]
 β   β£βββπlrc
 β   β£βββπscript
 β   ββββπsrt
 β£βββπsources  [ππ°πΆπ³π€π¦ π­πͺπ―π¬π΄]
 ββββπvrewld   [ππ³π’π―π΄π­π’π΅π¦π₯ π£πΊ ππ³π¦πΈ]
     β£βββπlrc
     ββββπsrt
```
Note that original files might not be from the original source, but from a different source (e.g. Vrew language interpreter, external transcriptors).

Parts inside subtitle folders only appear when necessary.
They are numbered following the original work's order.
This does not include the basic audio variations such as no SFX, no music, etc.

Source links generally refer to the original source for the transcript, but might also refer to the source for the audio files.
Tipical source sites are:
- π[Kikoeru ASMR one](https://www.asmr.one/works)π
- πΆ[EroVoice US](https://dl.erovoice.us/)πΆ
- πΊ[DLSite](https://www.dlsite.com/)πΊ

## Workflow
---
The workflow for obtaining a translation directory is as follows:
1. π§ Obtain the original files from the source if they are present. If not, create them from the audio files (e.g. using [Vrew](https://vrew.voyagerx.com/)).
2. π¬ Translate the original files using a tool of your choice (e.g. [DeepL](https://www.deepl.com/translator)).
3. π Convert the translated files to the desired format (e.g. `.srt`, `.lrc`), using a tool of your choice (e.g. [GoTranscript](https://gotranscript.com/subtitle-converter)).
4. π¨ Download the artwork from the source.
5. π Link the sources in the `sources` directory.

## Repository Structure
---
This repo has a private and a public mirror.
The public mirror is only missing the artwork folders and has some differences in utility files such as `.gitignore`.

Here I include how to update the public mirror, based on having two remotes named `origin` and `mirror`.
This assumes the existence of both a public and private repository in github, and the private repository is already locally cloned.
The idea is to have two branches, one with the `origin` remote and one with the `mirror` remote.

1. **Create the mirror public branch** 
```
git remote add mirror https://<username>@github.com/<username>/<private-repo-name>.git

git checkout -b public-temp
# delete artwork folders and other private-only files
git add *
git commit -m "init refactor"

# now we create an orhpan branch to remove the history
git checkout --orphan public
git branch -D public-temp
```
2. **Push the branch to the mirror remote**
```
# this pushes current branch to mirror:public
git push -u mirror public

# this sets the upstream of public to mirror:public
git branch public -u mirror/public
```
3. **Return to the private branch**
```
git checkout main
```
4. **Merge private π  public**
```
git checkout public
git checkout --theirs main <public_files>
# last checkout only transfers <public-files> from main to current branch, public

git commit -m "Publicate"
git push -u mirror public
```
5. **Merge private π  public**
```
git checkout public
git pull mirror <branch_in_mirror>
git checkout main
git checkout --theirs public <public_files>
git commit -m "Privatize"
git push origin main
```
6. **Note that checkouts may overwritten uncommited files, make sure to only checkout when branches are on HEAD**

All this commands should be implemented in a script or using git hooks.
In general, the structure is the following:
* We have 2 repos: private-repo and public-repo.
* In local we have 2 branches:
    * `main`: the private branch.
    * `public`: the public branch.
* In private-repo we have 1 branch:
    * `main`: remoted to `private-repo:main`.
* In public-repo we have 1 branch:
    * `public`: remoted to `public-repo:public`.
* There are 2 ways to update the repos:
    * `private-repo:main` π  `public-repo:public`
    * `private-repo:main` π  `public-repo:public`
* In both cases, we only want to update some files from the other branch, so we use `git checkout --theirs <from_branch> <files>`.

## Voice Works
---
See [here](archive/readme.md) a list of all the works in the archive.

You can update this repo by proposing a pull request with the new files, following the existing structure and updating the `archive/readme.md` file.

Special thanks to all those translators and transcriptors out there that make this possible.

*Please ignore the repo name, refer to audios as voice works instead.*