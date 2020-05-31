# OpenEdX Comprehensive theme auto install

* The playbook used by the script when it calls Ansible is *not applicable* for Vagrant devstack

## QUICK START

This guide describes how to set up automated install of themes

### REQUIREMENTS

Linux, [ansible](https://github.com/ansible/ansible).

#### Dependencies

* [x] ansible >=2.0.1.0
* [x] Ubuntu 12.04

### Step 1: Clone this repo

```bash
git clone https://github.com/mavaddat-javid-education/themex_script.git
```

### Step 2:  Run script

Enter repo directory

```bash
cd themex_script
```

#### When using a local zip file for theme

Use the local `-l` switch followed by the absolute path to the zip file for the theme (e.g., `theme-name.zip`).  

```bash
./update_theme.sh -l /some/local/zip-file/path/theme-name.zip
```

### When using a remote zip file for theme

Use the remote `-r` switch followed by the URL to the zip file for the theme (e.g., `theme-name.zip`).

```bash
./update_theme.sh -r http://themex.io/...../theme-name.zip
```

### When using theme branch in mavaddat-javid repo

Download theme from mavaddat-javid repo with specific branch, then supply the <span style="text-decoration: underline">b</span>ranch `-b` switch followed by the theme branch you want (e.g., `marvel-theme-eucalyptus`)

```bash
./update_theme.sh -b theme_branch
```

### When using your own theme repository

Use the <span style="text-decoration: underline">b</span>ranch <span style="text-decoration: underline">r</span>emote `-br` switch followed by the theme branch you want (e.g., `marvel-theme-eucalyptus`) and then the specific repository Git clone URL (suppose `theme_repo` represents the repository clone URL)

```bash
./update_theme.sh -br theme_branch theme_repo
```

### When setting up into some remote edX host

Use the <span style="text-decoration: underline">b</span>ranch <span style="text-decoration: underline">r</span>emote <span style="text-decoration: underline">h</span>ost `-brh` switch followed by the theme branch you want (e.g., `marvel-theme-eucalyptus`) and then the specific repository Git clone URL (suppose `theme_repo` represents the repository clone URL) followed by the URI for your host (e.g., an IP address for the server)

```bash
./update_theme.sh -brh theme_branch theme_repo edx_host
```

#### Specific Example

Let's suppose we want to install `marvel-theme-eucalyptus` branch from the specific repository https://github.com/mavaddat-javid-education/themes_for_themex.io.git into edX host server residing at IP address 200.83.1.109.
Then we use the <span style="text-decoration: underline">b</span>ranch <span style="text-decoration: underline">r</span>emote <span style="text-decoration: underline">h</span>ost `-brh` switch followed by the theme branch name, then the repo URL followed by the URI for our host. It would look like this:

```bash
./update_theme.sh -brh marvel-theme-eucalyptus https://github.com/mavaddat-javid-education/themes_for_themex.io.git 200.83.1.109
```

### Setting up a theme branch

Example

If you want to set up a theme branch (`theme_branch`) from a custom repo (`theme_repo`) into some group of edX hosts (`edx_host_group`), then **you'll need to modify the `inventory.ini` file** to list all the server addresses.

After that, use the <span style="text-decoration: underline">b</span>ranch <span style="text-decoration: underline">r</span>emote <span style="text-decoration: underline">h</span>ost with <span style="text-decoration: underline">i</span>nventory `-brhi` switch followed by the theme branch you want (e.g., `marvel-theme-eucalyptus`) and then the specific repository Git clone URL (`theme_repo` represents the repository clone URL) followed by the name for your edX server group

```bash
./update_theme.sh -brhi theme_branch theme_repo edx_host_group
```

#### Installing a specific theme

Example

Say we want to install `marvel-yellow-theme-eucalyptus` from https://github.com/mavaddat-javid-education/themes_for_themex.io.git into the group called `edx`. First, we modify our `inventory.ini` file:

```bash
echo -e "[edx]\n83.16.243.180\n69.176.165.155\n96.255.60.44\n40.192.240.83\n9.25.192.24\n77.62.109.78\n2.171.219.149\n27.27.157.234" >> inventory.ini
```

Then, we call the script with <span style="text-decoration: underline">b</span>ranch <span style="text-decoration: underline">r</span>emote <span style="text-decoration: underline">h</span>ost <span style="text-decoration: underline">i</span>nventory `-brhi` switch followed by `marvel-yellow-theme-eucalyptus` and then https://github.com/mavaddat-javid-education/themes_for_themex.io.git followed by `edx`:

```bash
./update_theme.sh -brhi marvel-yellow-theme-eucalyptus https://github.com/mavaddat-javid-education/themes_for_themex.io.git edx
```

In this case, `inventory.ini` file would contain

```ini
[edx]
83.16.243.180
69.176.165.155
96.255.60.44
40.192.240.83
9.25.192.24
77.62.109.78
2.171.219.149
27.27.157.234
```

#### If you use a configuration server

You will need to install [ansible](https://github.com/ansible/ansible) into whatever host in which you are running the script. For Ubuntu, it's

```bash
sudo apt-get update
sudo apt-get -y install software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update
sudo apt-get -y install ansible
```

If you are running a different OS, see the guide here: [Installing Ansible](https://github.com/ansible/ansible/blob/devel/docs/docsite/rst/installation_guide/intro_installation.rst)