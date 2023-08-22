
## I. Installing and Configuring Eclipse
### Downloading Eclipse
- [Eclipse Installer 2023-06 R | Eclipse Packages](https://www.eclipse.org/downloads/packages/installer)
### Installing Eclipse
- Choose **Eclipse IDE for Java Developers**
## II. Camelot Setup
### Windows
### MacOS
- Download the app from [here](https://drive.google.com/drive/folders/1iiD872kNDVB_G3Vk3O55cdb79iMAvGzI)(whole folder)
  ![[camelot_downloading_macos.png|500]]
- Locate the downloaded zip file (move it to your preferred location if you wish) and unzip it (e.g., at `~/Downloads/Camelot.app`)
- Open terminal at the app folder
  ![[macos_open_terminal.png|240]]
	- Change directory to the parent folder
    ```sh
    cd ..
    ```
	- Give execution permission to `Camelot.app` and change system policies (enter admin password when prompted) to allow applications downloaded from anywhere
    ```sh
    chmod -R +x Camelot.app
    sudo spctl --master-disable
    ```
	![[macos_app_anywhere.png|400]]
  ![[camelot_macos_setup.png|600]]
- Create a text file with name `StartExperienceManager.sh`
  ```sh
  open -a TextEdit StartExperienceManager.sh
  ```
  and edit it with the <ins>full path</ins> (e.g., `"/Users/username/Downloads/ManualExperienceManager.jar"`) of a required [`jar` file](https://tulane.instructure.com/courses/2271434/files/116767362)
  ```sh
  java -jar "/Full/Path/To/Your/JarFile.jar"
  ```
  ![[macos_get_full_path.png|320]]
### Launch Camelot
- Open Camelot ![[PlayerIcon.png|40]]
	- Enter `ShowMenu` in `Experience Manager`
	  ![[camelot_showmenu.png|400]]
> [!success]
> ![[camelot_start_screen.png|480]]
## III. Importing Class Project to Eclipse
- 

## IV. EGit Setup

## Links
- [Assignment Description](https://tulane.instructure.com/courses/2271434/assignments/14350002)
- [Configuring Camelot](https://tulane.instructure.com/courses/2271434/pages/configuring-camelot)