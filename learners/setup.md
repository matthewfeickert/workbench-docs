---
title: '101 Quick Start: Setting up your Workbench environment'
---

## Installation of the Workbench {#101-install}

The Workbench lesson infrastructure is built on Git, the R language, and pandoc.
It consists of four components:

1. The source content, i.e. the "lesson" (plain markdown or RMarkdown files organized into folders with a configuration yaml file)
2. The engine (R package [{sandpaper}]) to process the lesson content markdown to HTML
3. The validator (R package [{pegboard}]) to parse the source markdown files and highlight common errors
4. The renderer (R package [{varnish}]) to generate the final HTML, CSS, and JavaScript styling elements for the lesson website

Details of how these tools work together are explained in the [TODO](../episodes/todo.md).
In short, you can interact with the lesson source content and the Workbench tools to author and preview your lesson.

### What installation method should I choose?

We provide four mechanisms to interact with the Workbench:

- Devcontainers (online or local) **[recommended]**
  - We recommend using devcontainers as everything will be installed for you whether you are using an online or local environment, with minimal setup.
  - Lessons with devcontainer support will have a `.devcontainer` folder in the root of the repository.
  - **If no devcontainer is available for the lesson you wish to work on, please use the manual installation route, or Docker if you are comfortable with it.**
- Docker (local)
  - The Docker option can be useful for those that already have experience with Docker and containers, and are happy to do some manual configuration or wish to have more flexibility.
  - **Initial setup with docker is very straightfoward but can get complicated depending on your operating system!**
- Manual local installation from conda-forge with Pixi (local)
   - Installing all the requirements for development is one line and will create a fully reproducible environment.
  - **Initial setup with conda packages from conda-forge and Pixi is very straightfoward and is operating system agnostic.**
- Manual local installation with operating system specific tools (local)
  - Installing all the requirements manually on your local operating system is a longer process, but can be useful if you want to learn how to get an environment set up and will teach you more about the Workbench framework.
  - **If Docker and devcontainers are not suitable for you, installing things manually is a great option and still relatively quick to do!**
- GitHub (online)
  - Moving your development completely online by using GitHub's Codespaces or Dev environment is an excellent choice if you have fast internet and are comfortable with this process.
  - **Be advised that this option may incur a cost depending on your GitHub account status!**

::::::::::::::::::::: callout

### Why would I want to install locally if all these other options exist?

You can use the Workbench completely within devcontainers, Docker, or with [Pixi locally](#101-conda-forge), or through GitHub using our templates.

However, we still would recommend working through the [local setup instructions](#101-manual) at least once as they can save you a lot of time during lesson development and debugging in future.

:::::::::::::::::::::::::::::

## Devcontainers {#101-devcontainer}

Devcontainers are a way of remotely or locally setting up a coding environment based on a preconfigured "blueprint".
This blueprint is used by Integrated Development Environments (IDEs) like VSCode, vscodium, IDEA, or Zed, to initiate and configure an environment for you.
This can make it much quicker to get up and running with lesson development.

To use devcontainers you need:

- Docker: please read the [Docker installation instructions](#101-docker) to install Docker Desktop or the Docker Engine for your operating system.
- An IDE that supports devcontainers: We recommend [VSCode](https://code.visualstudio.com/) as it has the most complete and easy to set up devcontainer support. 
  We acknowledge that VSCode is free but not completely open source.

Please note, if you are not comfortable with using Docker for the Workbench, we recommend going through the [manual installation](#101-manual) steps below.

### Starting up the devcontainer

Make sure Docker Desktop is running and that you are connected to the Internet.

Open VSCode:

- either, by double clicking the icon in your OS, going to `File`, `Open Folder...`, and navigating to a lesson folder 
- or, open a terminal, navigate to a lesson folder and start VSCode by typing:

```bash
  cd ~/lessons/shell-novice
  code .
```

NB: Note the space between `code` and `.`!

Once VSCode has opened the folder, after a short time, a pop-up should appear in the bottom right of the IDE saying `Folder contains a Devcontainer configuration file. Reopen folder to develop in a container`, with an option button to `Reopen in container`.
Click this button and wait for VSCode to read the configuration file and setup the devcontainer environment.

:::::::::::::::::::: callout

### Troubleshooting

If this pop-up does not appear, open the command menu in VSCode with the <kbd>F1</kbd> function key.
Your cursor will appear in the command menu bar at the top of the window, prefixed with a `>` symbol.
Start typing `open folder` and select the `Dev Containers: Open Folder in Container...` option.

Similarly if you have any issues with the container at any point, you can open the command menu with <kbd>F1</kbd>, start typing `rebuild`, and select the `Dev Containers: Rebuild and Reopen in Container...`. This should be used judiciously as it will often reinstall dependencies so can take a few minutes.

::::::::::::::::::::::::::::

Various pop-ups will appear in the bottom right, showing progress.
You can click on the `Show log` link in any of the popups that show it to see any logs of the setup process.

The setup process can take a few minutes the first time you run it for a lesson.
After the first time, it will be much quicker to start subsequent uses of the environment as the Docker image would be downloaded and stored for reuse.

:::::::::::::::::::: callout

### Lessons with a lot of dependencies

For those R Markdown lessons that require a large number of R packages, this first start of the devcontainer can take quite a long time.

::::::::::::::::::::::::::::


### Running the Workbench

Open a terminal in VSCode by going to the `Terminal` menu in the top menu bar and click `New Terminal`.
An Ubuntu `bash` terminal window should appear in VSCode.
This bash shell will be running **inside** the devcontainer, so should look something like:

```bash
rstudio@55a86b63e4ab:~/lesson$ 
```

Here, you can perform any shell or R actions as you would usually for lesson development.

For more information, please check the full [devcontainer documentation](devcontainer.md).

::::::::::::::::::::: callout

### What if I don't want to use VSCode?

Sadly the devcontainer specification is only fully supported in a small number of IDEs.
VSCode is recommended in our lessons and it natively supports devcontainers.
Getting devcontainers to work in other fully open source IDEs like `vscodium` and `zed` are not as simple.

Therefore we would recommend using VSCode as whilst it is partially open source, it is a reliable and very well supported piece of software.

If this is not an option, then we recommend using the [Docker image directly](#101-docker) as it comes bundled with RStudio which you can use to work on your lesson.

**Sneaky extra:** If you want to run RStudio Server from VSCode, in a terminal shell running in the VSCode devcontainer, type:

```bash
~/start.sh
```

This will start the RStudio Server within the devcontainer, and you can then access RStudio by opening a web browser and going to `http://localhost:8787`. Fancy!

:::::::::::::::::::::::::::::

::::::::::::::::::::: callout

### Are devcontainers available for all lessons?

Devcontainer blueprints are already provided by our [workbench-template-rmd][rmd-template] and [workbench-template-md][md-template] lesson templates, so when creating a new lesson you will get access to devcontainers automatically.

However, not all Workbench-compatible lessons will have devcontainers enabled (a `.devcontainer` folder within the repository).
To add devcontainer support to a pre-existing lesson, please follow the [devcontainer import instructions TODO](../episodes/todo.md)

We will also be rolling these out into existing lessons across our official lesson programs too!

:::::::::::::::::::::::::::::


## Docker {#101-docker}

The documentation below for each operating system goes through how to manually install the Workbench dependencies, requirements, and packages.
To make this lengthy process shorter, the Workbench development team also provides Docker images of each release of the Workbench that are used for our GitHub workflows that build our core curriculum lessons.
You can use these Docker images to run the Workbench on your local system too!

Docker Desktop is available for all operating systems (Windows, Mac and Linux), so we recommend installing this.

### Docker Desktop

Install Docker Desktop for [your operating system](https://docs.docker.com/desktop/).

Once installed, choose one of the following ways to interact with the Docker system:

1. Via the Docker Desktop GUI app
2. Via the command line terminal (bash on Linux/Windows WSL/git bash, terminal on the Mac)

### Running the Workbench Docker container

After Docker Desktop/Docker Engine is set up, you can use the following command from the terminal (`git bash`, WSL, or MacOS Terminal app):

```bash
# go home
cd ~

# make a `lessons` folder in your home directory and clone in a lesson
mkdir ~/lessons
cd ~/lessons
git clone git@github.com:swcarpentry/shell-novice.git

# create a workbench-lessons named volume, and copy in the shell-novice content
curl -s https://raw.githubusercontent.com/carpentries/workbench-docker/main/scripts/setup_named_volume.sh | bash -s -- ~/lessons/shell-novice

# start the workbench container
curl -s https://raw.githubusercontent.com/carpentries/workbench-docker/main/scripts/run_workbench.sh | bash
```

Or with `docker run` directly, if you want to control various docker options:

```bash
docker run --name carpentries-workbench \
           -p 8787:8787 \
           -v ~/.ssh:/home/rstudio/.ssh:ro \
           -v ~/.gitconfig:/home/rstudio/.gitconfig \
           -e DISABLE_AUTH=true \
           -d carpentries/workbench-docker:latest
```

In the Docker Desktop app, you should see an entry appear in the "Containers" tab with the name `carpentries-workbench`.

You can now open a web browser and navigate to `http://localhost:8787` which will connect to the RStudio server running in the Docker container.
You're good to go!
Please continue with the [Test Your Installation](#install-test) instructions.

More information and docker runtime options are described in the [Docker guide](docker.md) and [Workbench developer docker documentation](https://github.com/froggleston/workbench-dev/blob/frog-docker-update-1/docker.qmd).

Please note, if you are not comfortable with Docker or the Workbench, we recommend going through the [manual installation steps](#101-manual) below.

## Manual Local Installation from conda-forge {#101-conda-forge}

:::::::::::::::::::: callout

### Computing platform agnostic

Installation from conda-forge is the same commands across all operating systems and computing architectures.

::::::::::::::::::::::::::::

All of the Workbench tools, and their dependencies, are packaged and distributed as built binaries in the form of conda packages on [conda-forge](https://conda-forge.org/) for Linux, macOS, and Windows.
You can setup an environment for lesson development that includes all dependencies (including R) with the following.

### With Pixi (recommended)

[Pixi](https://pixi.prefix.dev/) environments are fully reproducible by default.
From the project directory, initialize a Pixi workspace

```bash
pixi init
```

and then add Git and the Workbench tool packages (`r-pegboard` is a dependency of `r-sandpaper`)

```bash
pixi add git r-varnish r-sandpaper
```

You can optionally activate a shell with the environment loaded with

```bash
pixi shell
```

or execute all commands from within the environment with

```bash
pixi run <commands>
```

### With Conda

Create a [conda](https://docs.conda.io/) environment and install Git and The Workbench tool packages (`r-pegboard` is a dependency of `r-sandpaper`) from only the `conda-forge` channel

```bash
conda create --name workbench
conda config --name workbench --add channels conda-forge
conda config --name workbench --remove channels defaults
conda install --name workbench git r-varnish r-sandpaper
```

and then activate the conda environment

```bash
conda activate workbench
```

### Test your installation

To validate that you have all of the required tools installed in your environment

#### With Pixi (recommended)

Run from the command line in the project directory

```bash
pixi list
```

#### With Conda

Run from the command line

```bash
conda list --name workbench
```

and verify that `git`, `pandoc`, `r-base`, `r-pegboard`, `r-sandpaper`, `r-tinkr`, and `r-varnish` are listed.

## Manual Local Installation {#101-manual}

### Required Software {#101-required}

This setup document will take you through the process of installing or upgrading the required software on your local computer or server.

1. **[Git]** (&ge; 2.28 recommended)
2. **[R]** (&ge; 4.x)
3. **[pandoc]** (&ge; 3.x)
4. The lesson infrastructure R packages
   i. **[{sandpaper}]** (development version)
   ii. **[{varnish}]** (development version)
   iii. **[{pegboard}]** (development version)
   iiii. **[{tinkr}]** (markdown parser required by {pegboard})

   Once you have Git, R, and Pandoc installed, these packages can be installed and updated via:
   ```r
   install.packages(c("sandpaper", "varnish", "pegboard"),
     repos = c("https://carpentries.r-universe.dev/", getOption("repos")))
   ```

### Recommended Software {#101-recommend}

If you are using R or pandoc for the first time, we recommend using [the RStudio IDE][rstudio] for the following reasons:

1. It comes with [pandoc] pre-installed.
2. It works consistently across all major platforms.
3. It provides a dedicated `bash` terminal so you can easily switch between R and Git operations.
4. There are convenient keyboard shortcuts to preview lessons.
5. On Windows, it will automatically detect your R installation without you needing to edit your `PATH`.

If you do not want to use RStudio, that's perfectly okay and expected!
We want to you to be able work with the new template with the tools with which you're most familiar.
If you feel comfortable using a different tool (e.g. the command line or VSCode), then you should install R and pandoc separately and make sure that they are in your PATH.

If you already have software installed and are curious if you should update it to a newer version, the answer is almost always, yes.
Newer versions will often contain important bug fixes that are important to the security of your computer.

Jump to the installation instructions for your system: [Windows](#windows), [MacOS](#mac), or [Linux](#linux).

## Installing on Windows {#windows}

### Git

We recommend installing git via the [Git for Windows installer](https://gitforwindows.org/).
The installer is going to ask a lot of questions, so we recommend [following The Carpentries instructions for workshop participants](https://carpentries.github.io/workshop-template/#the-bash-shell).

#### Test your installation

To test that you have git installed, open your command line by pressing <kbd>Windows</kbd>+<kbd>R</kbd> and type `cmd` to bring up the command prompt.
From there, you can type `git --version` to see the version of your git installation.
You might see something like this:

```bash
git --version
```

```output
git version 2.31.1.windows.1
```

If, however, you see this error, then you should try to install git again.

```error
'git' is not recognised as an internal or external command, operable program or batch file.
```


### R

Install the [latest version of R for Windows](https://cran.r-project.org/bin/windows/base/).
There is also a video tutorial up on [The Carpentries instructions for workshop participants](https://carpentries.github.io/workshop-template/#r-1) that can be quite helpful for parsing the steps of installing R on Windows.

::::::::::::::::::::: callout

#### Optional: Want to add R to your PATH? {#winpath}

As we mention above, [we recommend using RStudio for your lesson](#recommend), but if you want to be able to integrate the lesson infrastructure into your own preferred workflow, you need to have R on your path.
The catch is that R for Windows does not automatically set your `PATH` variable. 

[Here are some instructions on setting up your PATH on Windows using both the GUI and CLI](https://www.maketecheasier.com/what-is-the-windows-path/).
Note that R will normally install at something like `C:\Program Files\R\R-4.4.0\bin\x64`, but if you are not an administrator on your device, it will install R in your `My Documents` folder.

To verify that R is installed in your `PATH`, open your command line by pressing <kbd>Windows</kbd>+<kbd>R</kbd> and type `cmd` to bring up the command prompt.
From there, you can type `R --version` at the prompt.
Your output should be similar to below, with a version ≥ 4.x.

```bash
R --version
```
```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-mingw32/x64 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

:::::::::::::::::::::::::::::

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Since pandoc comes bundled with RStudio, you can install it by installing the latest version of RStudio.
You can [download the installer from the RStudio website][rstudio].

#### Via the pandoc website

If you are comfortable adding R to your windows PATH (see [previous section](#winpath)), then you can install pandoc by using the download provided on its website at <https://pandoc.org/installing.html>

#### Test your installation

We will wait to test the pandoc installation after we have installed the infrastructure packages, to make sure it's discoverable by R.

### Infrastructure R packages

To install the R packages, you will need to **open RStudio** (or start R from the command line if you did not install RStudio) and enter the following lines into the console.

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard"))
```

## Installing on MacOS {#mac}

### Git

You should have git pre-installed on your macOS, but it is likely that this is an old version.
We recommend installing [The latest version of Git for MacOS](https://git-scm.com/downloads/mac). 
For a video guide, you can look at the [instructions for workshop participants](https://carpentries.github.io/workshop-template/#git-1).

#### Test your installation

To test your installation of Git and confirm it works, open **Terminal.app** and type the following:

```bash
git --version
```
```output
git version 2.31.0
```

If you have the default version of git, you might see this output, and that's okay for the purposes of this template.

```output
git version 2.24.3 (Apple Git-128)
```

### R

::: prereq

### Homebrew Not Recommended

Installing R via Homebrew can allow you to customise your installation, but you lose the advantage of having readily available package binaries.
Moreover, if you do not have the required C libraries (e.g. `libxslt`) installed, then the installation of some packages will fail.
So, unless you are prepared for this, **please do not use Homebrew to install R**.

:::


You can install the [latest R release][R] for MacOS from <https://cran.r-project.org/bin/macosx>.
There is also a video tutorial up on [The Carpentries instructions for workshop participants](https://carpentries.github.io/workshop-template/#rstats-macos) that can be quite helpful for parsing the steps of installing R on MacOS.

#### Test your installation

You can test your installation of R by opening **Terminal.app** and typing `R --version` into the prompt.
Your output should be similar to below, with a version ≥ 4.x:

```bash
R --version
```
```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin17.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Since pandoc comes bundled with RStudio, you can install it by installing the latest version of RStudio.
You can [download the installer from the RStudio website][rstudio].
RStudio will be a `*.dmg` (disk image) that you will double click to open a window that will look something like this:

![](fig/rstudio-mac-install.png){alt="Installation window for RStudio on mac showing two items on a plain background: the Applications folder on the left and the RStudio icon on the right."}

You should *drag the RStudio icon to the left, **into** the Applications folder* to install RStudio on your computer.

#### Via the pandoc website

If are more comfortable using R from the command line, then you can [install pandoc](https://pandoc.org/installing.html) by clicking the "Download the latest installer for macOS" button.
This will save a file called `pandoc-X.XX-macOS.pkg` installer to your computer.
Open the installer and follow the instructions to install pandoc on your computer.

#### Test your installation

We will wait to test the pandoc installation after we have installed the infrastructure packages, to make sure it's discoverable by R. 

### Infrastructure R packages

To install the R packages, you will need to **open RStudio** (or start R from the command line if you did not install RStudio) and enter the following lines into the console.

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = "https://cran.rstudio.com/"
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard"))
```

## Installing on Linux {#linux}

Instructions for installing on Linux are nuanced due to the variety and availability of libraries and dependencies for each distribution, e.g. Ubuntu is Debian based whereas Fedora is Red Hat based.
These instructions will use Ubuntu as the preferred distribution. 
The default `apt` repository is often out of date, so you will need to use a [Personal Package Archive aka PPA](https://itsfoss.com/ppa-guide/) to install the latest version of a particular software, which will be included in these instructions. 

### Git

Many distributions include git by default, but it is often outdated. 
It is useful to try to update in case a newer version is available:

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

#### Test your installation

Test your git installation by opening the terminal and running:

```bash
git --version
```
```output
git version 2.31.1
```

### R

To install R, you can visit [CRAN's Linux page](https://cran.r-project.org/bin/linux/) to check if your platform is supported.
Detailed instructions exist [for Ubuntu](https://cran.r-project.org/bin/linux/ubuntu/).
Here are the commands to register the PPA on your machine and then install R:

```bash
# update indices
sudo apt update -qq
# install two helper packages we need
sudo apt install --no-install-recommends software-properties-common dirmngr
# import the signing key (by Michael Rutter) for these repo
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
# add the R 4.0 repo from CRAN -- adjust 'focal' to 'groovy' or 'bionic' as needed
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"

# Install R
sudo apt install --no-install-recommends r-base
```

#### Test your installation

Test your R installation by opening your terminal and running  `R --version` into the prompt.
Your output should be similar to below, with a version ≥ 4.x:

```bash
R --version
```
```output
R version 4.1.0 (2021-05-18) -- "Camp Pontanezen"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.

```

### pandoc

There are two ways to install pandoc:

#### Via RStudio (recommended)

Pandoc comes bundled with RStudio.
You can [download the installer from the RStudio website][rstudio].
When installing RStudio for Linux, your distribution may not be shown on the landing page.
If your Ubuntu version is not listed, check the [RStudio Previous Versions](https://docs.posit.co/previous-versions/rstudio.html) page to see if there are builds available.

::::::::::: callout

### Optional: verify the install

You can optionally verify the download before installing by following the instructions at <https://posit.co/code-signing/>.

:::::::::::::::::::


#### Via the pandoc website

If you are more comfortable using R from the command line, then you can install pandoc from the [releases page](https://pandoc.org/installing.html).
From the list on the GitHub page, for Ubuntu, choose the appropriate `.deb` file for your chip architecture (i.e. AMD64 or ARM64).

#### Test your installation

We will wait to test the pandoc installation after we have installed the infrastructure packages, to make sure it's discoverable by R. 

### Infrastructure R packages

Linux packages normally need to be compiled into binaries by your system, which can take a long time the first time it happens.
RStudio provides a package manager that pre-compiles Linux binaries.
Note that you do not have to be using RStudio to take advantage of these binaries.
The one we are using is set up for the current Long Term Support (LTS) version of Ubuntu - 24.04 (noble).

::::: callout

#### Dependencies of Dependencies

If you are not used to installing software on Linux, it can be frustrating sometimes because things can go wrong and it’s not always immediately clear why.
The same is true for some R packages with compiled code.

Some packages require underlying C libraries (e.g. the xml2 library), which are catalogued for Ubuntu in [The Carpentries R Universe](https://carpentries.r-universe.dev/ui#builds) and [available via the API](https://carpentries.r-universe.dev/apis).
To produce a list (you may need to `sudo apt install jq` if it is not already on your system):

```bash
curl https://carpentries.r-universe.dev/stats/sysdeps 2> /dev/null | jq -r '.headers[0] | select(. != null)'
```

This list can be sent to `apt install` to install everything:

```bash
sudo apt-get install -y \
  $(curl https://carpentries.r-universe.dev/stats/sysdeps 2> /dev/null | jq -r '.headers[0] | select(. != null)') 2> /dev/null \
  || echo "Not on Ubuntu"
```

After you have these installed, you will be able to install the required R packages without error. 

:::::

:::: callout

#### What if I have a different version of Linux?

For the dependencies above, you can browse the [rstudio/r-system-requirements repository](https://github.com/rstudio/r-system-requirements) to find the correct formulation for your computer.

In addition, you should check [the supported operating systems for the Posit Package Manager](https://packagemanager.posit.co/__docs__/admin/serving-binaries/#supported-operating-systems) to see if you will benefit from pre-built binaries.

::::

To install the R packages, you will need to **open RStudio** (or start R from the command line if you did not install RStudio) and enter the following lines into the console:

```r
# Set the default HTTP user agent to get pre-built binary packages
RV <- getRversion()
OS <- paste(RV, R.version["platform"], R.version["arch"], R.version["os"])
codename <- sub("Codename.\t", "", system2("lsb_release", "-c", stdout = TRUE))
options(HTTPUserAgent = sprintf("R/%s R (%s)", RV, OS))

# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  CRAN = paste0("https://packagemanager.posit.co/all/__linux__/", codename, "/latest")
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard"))
```

::::::::::::: discussion

### Saving these settings for later

To not have to run this block of code every time you want to update, add the following code into your `~/.Rprofile` to run it every time you open your terminal:

::::::::::::::::::::::::

:::::: solution

### Add this to `~/.Rprofile`

Open the `nano` text editor:

```bash
nano ~/.Rprofile
```

And copy and paste the following code at the bottom of the file. Once you have done so, type <kbd>Ctrl</kbd>+<kbd>X</kbd> to save and exit.

```r
local({
  # Set the default HTTP user agent to get pre-built binary packages
  RV <- getRversion()
  OS <- paste(RV, R.version["platform"], R.version["arch"], R.version["os"])
  codename <- sub("Codename.\t", "", system2("lsb_release", "-c", stdout = TRUE))
  options(HTTPUserAgent = sprintf("R/%s R (%s)", RV, OS))

  # register the repositories for The Carpentries and CRAN
  options(repos = c(
    carpentries = "https://carpentries.r-universe.dev/",
    CRAN = paste0("https://packagemanager.posit.co/all/__linux__/", codename, "/latest")
  ))
})
```
:::::::::::::::


::::::::::::: callout

### What if I get errors installing packages?

If you run into errors (non-zero exit status), it probably means that you were missing a C library dependency that needs to be installed via your package manager (i.e. apt).
To resolve these issues, scroll back in the log and you might find messages that looks similar to this:

```output
* installing *source* package ‘xslt’ ...
** using staged installation
Package libexslt was not found in the pkg-config search path.
Perhaps you should add the directory containing `libexslt.pc'
to the PKG_CONFIG_PATH environment variable
No package 'libexslt' found
Using PKG_CFLAGS=-I/usr/include/libxml2
Using PKG_LIBS=-lexslt -lxslt -lxml2
-----------------------------[ ANTICONF ]-------------------------------
Configuration failed to find libexslt library. Try installing:
 * deb: libxslt1-dev (Debian, Ubuntu, etc)
 * rpm: libxslt-devel (Fedora, CentOS, RHEL)
 * csw: libxslt_dev (Solaris)
If libexslt is already installed, check that 'pkg-config' is in your
PATH and PKG_CONFIG_PATH contains a libexslt.pc file. If pkg-config
is unavailable you can set INCLUDE_DIR and LIB_DIR manually via:
R CMD INSTALL --configure-vars='INCLUDE_DIR=... LIB_DIR=...'
---------------------------[ ERROR MESSAGE ]----------------------------
<stdin>:1:10: fatal error: libxslt/xslt.h: No such file or directory
compilation terminated.
------------------------------------------------------------------------
```

Use the instructions in these logs to install the correct package from your terminal and then open R or RStudio and retry installing the packages.
For example, for the error above, use `sudo apt install libxslt1-dev`.

:::::::::::::::::::::


## Test your Workbench installation {#install-test}

To test your installation **open RStudio** either as the locally installed app or in the browser if using Docker (or launch R if you have not installed RStudio and are not using Docker/devcontainers) and enter the following commands to confirm everything works:

```r
rmarkdown::pandoc_version()
tmp <- tempfile()
sandpaper::no_package_cache()
sandpaper::create_lesson(tmp, open = FALSE)
sandpaper::build_lesson(tmp, preview = FALSE, quiet = TRUE)
fs::dir_tree(tmp, recurse = 1)
```

```output
[1] '3.10.2'
ℹ Consent for package cache revoked. Use `use_package_cache()` to undo.
→ Creating Lesson in '/tmp/RtmpnRjHyr/file12f34734be05f'...
✔ First episode created in '/tmp/RtmpnRjHyr/file12f34734be05f/episodes/01-introduction.Rmd'
ℹ Workflows up-to-date!
✔ Lesson successfully created in '/tmp/RtmpnRjHyr/file12f34734be05f'
/tmp/RtmpnRjHyr/file12f34734be05f
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── README.md
├── config.yaml
├── episodes
│   ├── 01-introduction.Rmd
│   ├── data
│   ├── fig
│   └── files
├── index.md
├── instructors
│   └── instructor-notes.md
├── learners
│   └── setup.md
├── profiles
│   └── learner-profiles.md
└── site
    ├── DESCRIPTION
    ├── README.md
    ├── _pkgdown.yaml
    ├── built
    └── docs
```

If the installation did not work, please [raise an issue on GitHub](https://github.com/carpentries/workbench/issues/new). 

## Connect to GitHub

You will need to make sure your git session is connected to GitHub.
To do so, you will need to use an SSH or HTTPS protocol.
If you already know how to push and pull from GitHub using the command line, you do not need to worry about setting this up.

:::::::::::::::: callout

### Docker/devcontainers and git

If you already have your git installation configured outside the Docker/devcontainer environment, the various scripts and commands used in this documentation include mapping your local SSH (and GPG signing) configuration into the container.
This means your git commands should "just work" inside the container as they would outside.

If you have any issues, please open an issue on the [workbench-docker](https://github.com/carpentries/workbench-docker/issues) GitHub repo and/or ask for help on the `workbench` channel in [The Carpentries Slack workspace](https://carpentries.org/community/get-involved/).

::::::::::::::::::::::::

If you do not have this set up, you should [choose a protocol](https://docs.github.com/en/github/getting-started-with-github/about-remote-repositories) and then set them up according to the instructions from GitHub.

It’s recommended to use the SSH protocol, unless you explicitly cannot, e.g. behind an institutional firewall or proxy.

:::::::::::::::: callout

### Is GitHub's Documentation Confusing?

You may find GitHub's documentation slightly confusing and/or lacking.
The following resources are extremely helpful for setting up authentication credentials for your account:

[Remotes in GitHub (Software Carpentry)](https://swcarpentry.github.io/git-novice/07-github)
: A walkthrough of creating a repository on GitHub and pushing to it via the command line.

[Connect to GitHub (Happy Git With R)](https://happygitwithr.com/push-pull-github.html)
: A walkthrough of creating a throwaway repository that gives you a good idea for the mechanics of working with GitHub.

[Cache credentials for HTTPS (Happy Git With R)](https://happygitwithr.com/credential-caching.html)
: Clear explanation on how to set up a Personal Access Token and the benefits of using HTTPS. This explains how to do this in both the shell and R.

[Set up keys for SSH (Happy Git With R)](https://happygitwithr.com/ssh-keys.html)
: Clear explanation on what SSH key pairs are and how to set up and connect them with GitHub. This has recommendations using both the shell and RStudio.

::::::::::::::::::::::::

[Git]: https://git-scm.com/
[R]: https://cran.rstudio.org/
[pandoc]: https://pandoc.org/
[{tinkr}]: https://docs.ropensci.org/tinkr/
[rmd-template]: https://github.com/carpentries/workbench-template-rmd
[md-template]: https://github.com/carpentries/workbench-template-md
[^workspace]: By default, R will ask if you want to save your workspace to a
  hidden file called `.RData`. This is loaded when you start R, restoring your
  environment with all of the packages and objects you had previously loaded.
  This default behavior is not good for reproducibility and makes updating
  packages very very difficult. In 2017 Jenny Bryan wrote a very good article
  about the benefits of having a project-based workflow, starting from a clean
  slate: <https://www.tidyverse.org/blog/2017/12/workflow-vs-script/>
