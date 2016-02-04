# OpenLMIS Git-Repo Manifest
This is the default OpenLMIS git-repo manifest.  

*This repository and the git-repo tool is currently expirementally being used 
for OpenLMIS 2.0 for limited modularity support*

## Adding a new module to OpenLMIS

1. Install and familiarize yourself with 
[git-repo](https://code.google.com/p/git-repo/).
2. Make a directory for OpenLMIS and init repo within it:
  
  ```shell
  > mkdir openlmis
  > cd openlmis
  > repo init -u https://github.com/OpenLMIS/openlmis-repo
  ```
3. If you don't have permissions to contribute directly to OpenLMIS on GitHub, 
create a fork for potential future pull-requests, then reference your forked
repository in a local manifest of git-repo:
  1. create local manifest dir:

    ```shell
    > mkdir .repo/local_manifests
    > touch .repo/local_manifests/forked_openlmis.xml
    ```
  2. in `forked_openlmis.xml` reference your fork (replace <yourUserName>
  with your GitHub account):

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <manifest>
      <remote name="forked-origin" fetch="https://github.com/<yourUserName>"/>
      <remove-project name="open-lmis"/>
      <project name="open-lmis"
        revision="dev"
        remote="forked_origin"
        path="."/>
    </manifest>
    ```
4. Download OpenLMIS & standard module sources:
  
  ```shell
  > repo sync
  track OpenLMIS dev branch (for non-forked projects):
  > git checkout --track openlmis-origin/dev
  OR if you're on a forked OpenLMIS (see step 3):
  > git checkout --track forked-origin/dev
  ```
5. Create a new module and write your source by following the instructions in 
the [module-template](https://github.com/OpenLMIS/module-template) project.
6. Manage your new module with repo by adding it to your local-manifest.  e.g.:
  1. Ensure your local-manifest directory exists `mkdir .repo/local_manifests/`
  2. Make a manfiest file for your module `deliver` in 
  `.repo/local_manifests/deliver.xml`:
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <manifest>
      <remote name="github" fetch="https://github.com/"/>
      <default revision="refs/heads/master"
        remote="github"/>
      <project name="<yourUserName>/deliver"
        remote="github"
        path="modules/deliver"/>
    </manifest>
    ```
    *replace `yourName` with the account name you have your module at.  
    e.g. https://github.com/yourName/deliver*
7. Customize your manifest further so that you properly commit sources to your
modules while still tracking OpenLMIS for the latest and greatest.

