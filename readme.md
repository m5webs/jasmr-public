# jasmr
jasmr directory of translations for DLSite ASMR works.

## Archive Structure
---
```
📦example
 ┣━━━📂artwork  [𝘈𝘳𝘵𝘸𝘰𝘳𝘬 𝘧𝘪𝘭𝘦𝘴]
 ┣━━━📂deepld   [𝘛𝘳𝘢𝘯𝘴𝘭𝘢𝘵𝘦𝘥 𝘣𝘺 𝘋𝘦𝘦𝘱𝘓]
 ┃   ┣━━━📂lrc
 ┃   ┃   ┣━━━📂part1
 ┃   ┃   ┗━━━📂part2
 ┃   ┗━━━📂srt
 ┣━━━📂original [𝘖𝘳𝘪𝘨𝘪𝘯𝘢𝘭 𝘧𝘪𝘭𝘦𝘴]
 ┃   ┣━━━📂lrc
 ┃   ┣━━━📂script
 ┃   ┗━━━📂srt
 ┣━━━📂sources  [𝘚𝘰𝘶𝘳𝘤𝘦 𝘭𝘪𝘯𝘬𝘴]
 ┗━━━📂vrewld   [𝘛𝘳𝘢𝘯𝘴𝘭𝘢𝘵𝘦𝘥 𝘣𝘺 𝘝𝘳𝘦𝘸]
     ┣━━━📂lrc
     ┗━━━📂srt
```
Note that original files might not be from the original source, but from a different source (e.g. Vrew language interpreter, external transcriptors).

Parts inside subtitle folders only appear when necessary.
They are numbered following the original work's order.
This does not include the basic audio variations such as no SFX, no music, etc.

Source links generally refer to the original source for the transcript, but might also refer to the source for the audio files.
Tipical source sites are:
- 💞[Kikoeru ASMR one](https://www.asmr.one/works)💞
- 🎶[EroVoice US](https://dl.erovoice.us/)🎶
- 🌺[DLSite](https://www.dlsite.com/)🌺

## Workflow
---
The workflow for obtaining a translation directory is as follows:
1. 🎧 Obtain the original files from the source if they are present. If not, create them from the audio files (e.g. using [Vrew](https://vrew.voyagerx.com/)).
2. 💬 Translate the original files using a tool of your choice (e.g. [DeepL](https://www.deepl.com/translator)).
3. 📝 Convert the translated files to the desired format (e.g. `.srt`, `.lrc`), using a tool of your choice (e.g. [GoTranscript](https://gotranscript.com/subtitle-converter)).
4. 🎨 Download the artwork from the source.
5. 🔖 Link the sources in the `sources` directory.

## Repository Structure
---
This repo is private and has a public mirror.
The public mirror is only missing the artwork folders and has some differences in utility files such as `.gitignore` and `README.md`.

Here I include how to update the public mirror, based on having two remotes named `origin` and `mirror`, and a private branch.
This assumes the existence of both a public and private repository in github, and the private repository is already locally cloned.

1. **Create the mirror and branch** 
```
git remote add mirror https://<username>@github.com/<username>/<private-repo-name>.git

git checkout --orphan public
```
2. **Make changes on the public branch and push to main repo**
```
git push -u origin public
```
3. **Push the branch to the mirror remote**
```
git push -u mirror public
//this pushes to mirror:public

git branch public -u mirror/public
//this sets the upstream of public to mirror:public
```
1. **Return to the private branch**
```
git checkout main
```
1. **Merge private 🠊 public**
```
git checkout public
git checkout --patch main <files> 
//remove --patch if files do not exist in public

git push -u mirror public
```
6. **Merge private 🠈 public**
```
git checkout public
git pull mirror <branch-in-mirror>
git push -u origin public

//make a pull request from public to main in github's private repo
```
7. **Fetch changes from origin:public**
```
git checkout public
git pull origin public
git push -u mirror public
```
All this commands should be implemented in a script or using git hooks.
In general, the structure is the following:
* We have 2 repos: private-repo and public-repo.
* In private-repo we have 2 branches:
    * `main`: the private branch.
    * `public`: the public branch.
* In public-repo we have 1 branch:
    * `public`: synced with `private-repo:public`.
* There are 2 ways to update the repos:
    * `private-repo:main` 🠊 `private-repo:public` 🠊 `public-repo:public`
    * `private-repo:main` 🠈 `private-repo:public` 🠈 `public-repo:public`
* In the first case, we want to exclude some files from the private branch, so we use `git checkout --patch main <files>`.

## Status and Assignments
---
**Archive structure**
* Rename `deepld/LRC` number-only files:
    - [x] RJ271132

**Missing data**
* In the archive:
    - [x] None
* To be imported:
    - [ ] etc. (See `archive/readme`)
