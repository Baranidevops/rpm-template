# devops-generic-rpm-template

This template uses the [cookiecutter](http://cookiecutter.readthedocs.io/en/latest/index.html) command line utility.

## Create your own RPM gradle project repository (using the [Nebula gradle-ospackage-plugin](https://github.com/nebula-plugins/gradle-ospackage-plugin/blob/master/Plugin-Rpm.md)) based off this template

### 1) Install cookiecutter
```
[sudo] pip install cookiecutter
```
or
```
brew install cookiecutter
```
---
### 2) Generate your RPM project via cookiecutter (2 options below - PICK EITHER ONE)
##### Using the command line prompts to fill in template
- Run the following command to use the devops-generic-rpm-template git repo as the template base
**(Note: this will create a new directory in whatever directory you are currently in)**
```
cookiecutter git@git.devops.com:cpe-rpm/devops-generic-rpm-template.git
```

- Follow the command line prompts to create your specific rpm project
**Note: some of the prompts have defaults, you may keep these defaults by pressing 'enter', otherwise you can override them with your own text input.**

---

##### Using a yaml configuration file to set the template attributes
##### Note :-  There is an attribute within this template to switch between drone & Jenkins (attribute = "jenkins_or_drone")
- Create a configuration yaml file with the settings of your choice on your local machine (see [sapphire-config-example.yaml](sapphire-config-example.yaml)) as an example.
**Note: you need to have the ```default_context:``` at the top of the yaml file. See the [advanced usage documentation](https://github.com/audreyr/cookiecutter/blob/9ded8b172929619f1b3a2c1842d37e8beca25f24/docs/advanced_usage.rst) for more help.** Once you have created your config yaml file, run the following command:
```
cookiecutter --no-input --config-file /path/to/config/yaml/file/filename.yaml git@git.devops.com:cpe-rpm/devops-generic-rpm-template.git
```
**Once again, note that this will create your new templated project directory in whatever directory you're currently in.**

---
## Configuration Attributes

You can see all of the available options in the [cookiecutter.json](cookiecutter.json) file.

```app_name```: Name of the application. The default config will use the app_name to generate the ```repo_name```.

```app_component_name```: Name of the application component. Will be appended to the ```repo_name```. Defaults to an empty string.

```repo_name```: Name of the repository. This is used for the output project directory name as well as the name of the gradle project as seen in the settings.gradle file. Default convention will append a 'devops-' prefix to the ```app_name``` attribute followed by '-```app_component_name```'and convert all spaces to hyphens. This will set the rootProject.name gradle project property for use throughout the gradle project and it will set the name of the project's root directory - this will also be used as the rpmName.

```gradle_version```: Version of gradle for the gradle wrapper. Defaults to 2.12.

```rpm_publish_artifactory_url```: URL that will be used to publish the resulting RPM artifact. Defaults to 'https://binrepo.devops.com/artifactory'. This will set the artifactoryUrl gradle project property for use throughout the gradle project.

```apply_download_source_plugin```: Flag to indicate whether the download source plugin will be used in the project. This is necessary to download the source files. Defaults to 'false'. This will determine whether a downloadSource task is included in the project, when an external source file (such as a .zip or .tar.gz or a .jar) needs to be downloaded.

```source_artifact_url```: URL that will be used to download the source artifact - which will be packaged in the RPM. Defaults to 'https://binrepo.devops.com/artifactory'. This will set the sourceArtifactoryUrl gradle project property for use throughout the gradle project - this is used in particular when the apply_download_source_plugin property is set to true.

```source_artifact_repo```: Repository name of the source artifact. Prompts user for input - dummy default is '<INSERT_SOURCE_ARTIFACT_REPO_NAME>'. This will set the sourceArtifactRepository gradle project property for use throughout the gradle project - this is used in particular when the apply_download_source_plugin property is set to true.

```source_artifact_path```: Path of the source artifact. Prompts user for input - dummy default is '<INSERT_SOURCE_ARTIFACT_PATH>'. This will set the sourceArtifactPath gradle project property for use throughout the gradle project - this is used in particular when the apply_download_source_plugin property is set to true.

```source_artifact_version```: Version of the source artifact. Prompts user for input - dummy default is '<INSERT_SOURCE_ARTIFACT_VERSION>'. This will set the sourceArtifactVersion gradle project property for use throughout the gradle project - this is used in particular when the apply_download_source_plugin property is set to true.

```source_artifact_name```: Name of the source artifact. Prompts user for input - dummy default is '<INSERT_SOURCE_ARTIFACT_NAME>'. Must include file extension. This will set the sourceArtifactName gradle project property for use throughout the gradle project - this is used in particular when the apply_download_source_plugin property is set to true.

```rename_source_artifact```: Flag to indicate whether the downloaded source artifact should be renamed from the original source name. Defaults to 'false'.

```renamed_source_artifact_name```: Name to use for renaming the source artifact. Must include the file extension. Defaults to an empty string. This will set the finalSourceArtifactName gradle project property for use throughout the gradle project only when the rename_source_artifact is set to 'true'.

```yum_artifactory_publish_repo```: Name of the repository to which the resulting RPM will be published. Defaults to 'cpe-yum-local'. This will set the yumArtifactoryPublishRepository gradle project property for use throughout the gradle project.

```include_preinstall_script```: Flag to indicate whether a preinstall script will be used for the RPM. Defaults to 'false'.

```include_postinstall_script```: Flag to indicate whether a postinstall script will be used for the RPM. Defaults to 'false'.

```rpm_dependencies```: Comma separated list of RPMs that the project's output RPM depends on. Defaults as an empty string. This will set the rpmDependencyString gradle project property for use throughout the gradle project.

---

### **Final Disclaimer: this template will generate the default files/configuration for creating a generic RPM - you are encouraged to change the resulting project in any way that you need.**
