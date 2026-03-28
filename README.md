# Setting up NFS, MinIO, and an Nginx Reverse Proxy

## Project Overview

As part of this lab, two practical tasks were completed:

1. A file server based on **NFS** was configured to allow remote directory mounting over the network between two virtual machines.
2. **MinIO** object storage was deployed, a user bucket was created, access permissions were configured, and static content was published through an **Nginx reverse proxy**.

This project covers several important system administration topics at once: network file systems, object storage, user and access policy management, publishing content through a web server, and basic inter-server integration.

## Objectives

- deploy and configure an NFS server;
- connect an NFS resource on a client machine;
- set up MinIO object storage;
- create a user, bucket, and access policy;
- upload files to MinIO;
- expose static content through an Nginx proxy;
- strengthen practical skills in working with Linux services, network protocols, and configuration files.

## Technologies Used

- **Linux**
- **NFS**
- **MinIO**
- **mc (MinIO Client)**
- **Nginx**
- **systemd**
- **wget**

## Project Architecture

The project uses two virtual machines:

### Part 1. NFS
- **VM1** — NFS server
- **VM2** — NFS client

### Part 2. MinIO + Nginx
- **VM1** — server running MinIO
- **VM2** — server running Nginx, proxying requests to MinIO

## Completed Tasks

### 1. NFS Server Configuration

On the server machine, the following steps were completed:
- installed the `nfs-kernel-server` and `nfs-common` packages;
- created the shared directory `/srv/share/nfs`;
- configured the `/etc/exports` file to provide network access with read and write permissions;
- verified exported directories using `showmount -e localhost`.

### 2. Mounting the NFS Directory on the Client

On the client machine, the following steps were completed:
- installed the `nfs-common` package;
- created the mount point `/mnt/share`;
- mounted the remote directory from the server VM locally;
- created a test file named `nfs-practice`;
- configured automatic mounting through `/etc/fstab` if needed.

### 3. MinIO Deployment

On the MinIO server, the following actions were performed:
- installed MinIO;
- created a dedicated system user `minio-user` and a group;
- prepared the working directory `/media/minio`;
- configured the `/etc/default/minio` file;
- enabled access to the web console on port `9001`;
- installed the `mc` client for storage administration.

### 4. Configuring Users, Buckets, and Policies in MinIO

After starting MinIO, the following tasks were completed:
- connected the `mc` client to the server;
- created the user `minio-<username>`;
- created a personal bucket;
- created and assigned an access policy with full permissions for the bucket and its contents;
- uploaded a test file named `minio-practice`.

### 5. Publishing Static Content

To demonstrate public access, the following steps were completed:
- created an additional bucket `myminio/static`;
- uploaded an HTML page `index.html`;
- enabled anonymous access to the bucket;
- verified that static content was served correctly from MinIO.

### 6. Nginx Reverse Proxy Configuration

On the second virtual machine, the following actions were completed:
- installed Nginx;
- modified the configuration file `/etc/nginx/sites-available/default`;
- configured request proxying to the static `index.html` object stored in MinIO;
- verified page access through a browser.

## Verification

The following items were prepared and checked during the task:

### For NFS
- contents of `/etc/exports`;
- output of `showmount -e localhost`;
- output of `ls -l` inside the mounted directory;
- if available, contents of `/etc/fstab`.

### For MinIO and Nginx
- contents of `/etc/default/minio`;
- output of `mc admin info myminio`;
- output of `mc admin policy info myminio minio-<username>-policy`;
- output of `mc admin user info myminio minio-<username>`;
- bucket and file availability through the web interface;
- configuration of `/etc/nginx/sites-available/default`;
- correct opening of the `index.html` page in a browser.

## Result

As a result of this work, the following setup was successfully implemented:

- one virtual machine acts as an NFS file server;
- the second machine mounts a remote directory over the network;
- MinIO is used as object storage;
- users, buckets, and access policies were configured;
- static HTML content was published through an Nginx proxy.

This project helped reinforce practical skills in working with network file systems, object storage, Linux services, and web proxy configuration.
