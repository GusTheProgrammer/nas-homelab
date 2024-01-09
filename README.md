<a name="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/GusTheProgrammer/nas-homelab">
    <img src="https://icones.pro/wp-content/uploads/2022/07/symbole-de-bus-jaune.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">Synology NAS Homelab</h3>

  <p align="center">
    A docker compose file for everything

</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#Running-with-Portainer">Running with Portainer</a></li>
        <li><a href="#Docker-Compose">Docker Compose</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#Documentation">Documentation</a></li>

  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

This project aims to provide a comprehensive Docker Compose setup for a versatile homelab environment. It includes services for reverse proxy, media management, DNS blocking, and more, all managed through Docker on a Synology NAS. This setup is designed to be both robust and flexible, catering to various home server needs.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

[![Docker][Docker]][Docker-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->

## Getting Started

To get your homelab up and running, follow these steps:

### Running with Portainer

1. **Install Portainer:**

   - Run [Portainer](https://docs.portainer.io/start/install-ce/server/docker/linux) on Docker with the following command:
     ```sh
     docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
     ```

2. **Create Folder Structure:**

   - Create these folders as per the tree below:
     ```
        /volume1/
        ├── docker/
        │   └── homelab/
        │       ├── data (for Nginix Proxy Manager | It's not happy sometimes when u change the folder name 🤷‍♂️)
        │       ├── letsencrypt (also for Nginix Proxy Manager)
        │       ├── overseerr-data
        │       ├── vw-data
        │       ├── homarr/
        │       │   ├── configs
        │       │   ├── data
        │       │   └── icons
        │       ├── radarr
        │       ├── sonarr
        │       ├── lidarr
        │       ├── readarr
        │       ├── bazarr
        │       ├── prowlarr
        │       ├── maintainerr
        │       ├── qbit
        │       ├── vuetorrent (Optional)
        │       ├── dash
        │       ├── etc-pihole
        │       ├── etc-dnsmasq.d
        │       └── home-assistant
        └── homelab-media/
            ├── media/
            │   ├── books
            │   ├── movies
            │   ├── music
            │   └── tv
            └── torrents/
                ├── books
                ├── movies
                ├── music
                └── tv
     ```

3. **Using Portainer:**

   - Access Portainer by navigating to `https://[your-nas-ip-address]:9000`.
   - Log in and go to the 'Stacks' section.
   - Add a new stack. You can either:
     - Paste the content of your Docker Compose file directly, or
     - Use the URL of your GitHub repository containing the Docker Compose file.

4. **Set Up Environment Variables:**

   - In Portainer, you can set environment variables for each service under the stack configurations.

   ```
    VAULTWARDEN_ADMIN_TOKEN
    VAULTWARDEN_SMPT_HOST
    VAULTWARDEN_SMTP_FROM
    VAULTWARDEN_SMTP_USERNAME
    VAULTWARDEN_SMTP_PASSWORD
    PIHOLE_PASSWORD
   ```

### Docker Compose

1. **Prerequisites:**

   - Ensure Docker is installed on your Synology NAS.
   - Ensure the same Folder structure from the previous method.

2. **Clone the Repository (Optional):**

   - If your configuration is in a Git repository, clone it:
     ```sh
     git clone https://github.com/GusTheProgrammer/nas-homelab.git
     ```
   - Navigate to the directory containing the `docker-compose.yml` file.

3. **Create the network**
   - Run this command before you start the Docker Compose file:
     ```sh
      docker network create homelab
     ```
4. **Running the Services:**
   - Start the services using Docker Compose:
     ```sh
     docker-compose up -d
     ```
   - Make sure to set the necessary environment variables in your `docker-compose.yml` file or as a separate `.env` file in the same directory.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

After the stack is up and running you should go into each service and configure them to your liking.

In this configuration `Nginx Proxy Manager` is configured to ports `8341` & `8766` since the default `80` and `443` are taken by Synology for their QuickConnect services.

Your port forwading rules should be something like this:

- External Port `80` ➡️ Internal Port `8341`
- External Port `443` ➡️ Internal Port `8766`

or whatever you choose to set these ports to.

## Documentation

### NOTE❗ When in doubt always referr back to [TRaSH Guides](https://trash-guides.info/)

- [Nginx Proxy Manager](https://nginxproxymanager.com/guide/#project-goal)
- [Vaultwarden](https://github.com/dani-garcia/vaultwarden/wiki)
- [Overseerr](https://docs.overseerr.dev/)
- [Homarr](https://homarr.dev/docs/getting-started/prerequisites)
- [Radarr](https://wiki.servarr.com/en/radarr)
- [Sonarr](https://wiki.servarr.com/sonarr)
- [Lidarr](https://wiki.servarr.com/en/lidarr)
- [Readarr](https://wiki.servarr.com/en/readarr)
- [Bazarr](https://wiki.bazarr.media/)
- [Prowlarr](https://wiki.servarr.com/en/prowlarr)
- [Maintainerr](https://github.com/jorenn92/Maintainerr/blob/main/docs/2-getting-started/1-installation/Installation.md)
- [qBittorrent](https://github.com/linuxserver/docker-qbittorrent)
- [VueTorrent](https://github.com/WDaan/VueTorrent) Alternative look for qBittorrent WebUI (Optional)
- [Dash](https://getdashdot.com/docs/install)
- [Pihole](https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker)
- [Home Assistant](https://www.home-assistant.io/docs/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[Docker]: https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white
[Docker-url]: https://www.docker.com/
