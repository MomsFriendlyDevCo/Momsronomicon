Hosting Node Environments
=========================
Setting up a Node environment generally follows the below stages:

1. Setup of Linux LTS distribution (Ubuntu / Debian preferred)
2. Update of core security packages to latest releases
3. Installation of additional packages
4. Provisioning of NodeJS suitable environment (PPA installation + NPM configuration)
5. Provisioning of MongoDB suitable environment (PPA Installation + WiredTiger DB engine configuration)
6. Security installation (Firewall, Auto-security updates, SSH lockdown)
7. Code cloning into server
8. Web server setup (site compile, minification, PM2 installation)


Setup walkthough
----------------
The majority of the above stages are automated via the [MFDC Init](https://github.com/MomsFriendlyDevCo/Init) project.

**1. Dial into the server**

```
ssh <server name here>
```


**2. Install base libraries**

```
sudo apt-get -y install git wget
```


**3. Clone Init to the server**

```
git clone https://github.com/MomsFriendlyDevCo/Init.git
```

**4. Run the ROLE-server-node script**

```
cd Init
./ROLE-server-node
```

From this point on the installation sequence should be automated.

If prompted answer `Internet` to the PostFix mail daemon setup.



**[Back to Table of Contents](../README.md)**
