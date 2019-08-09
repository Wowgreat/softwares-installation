### Summarize from official page

- **requirements**

  | Resource | Capacity      | Description        |
  | -------- | ------------- | ------------------ |
  | CPU      | minimal 2 CPU | 4 CPU is preferred |
  | Mem      | minimal 4GB   | 8GB is preferred   |
  | Disk     | minimal 40GB  | 160GB is preferred |

  | Software       | Version                       | Description                                                  |
  | -------------- | ----------------------------- | ------------------------------------------------------------ |
  | Docker engine  | version 17.06.0-ce+ or higher | For installation instructions, please refer to: [docker engine doc](https://docs.docker.com/engine/installation/) |
  | Docker Compose | version 1.18.0 or higher      | For installation instructions, please refer to: [docker compose doc](https://docs.docker.com/compose/install/) |
  | Openssl        | latest is preferred           | Generate certificate and keys for Harbor                     |

  | Port | Protocol | Description                                                  |
  | ---- | -------- | ------------------------------------------------------------ |
  | 443  | HTTPS    | Harbor portal and core API will accept requests on this port for https protocol, this port can change in config file |
  | 4443 | HTTPS    | Connections to the Docker Content Trust service for Harbor, only needed when Notary is enabled, This port can change in config file |
  | 80   | HTTP     | Harbor portal and core API will accept requests on this port for http protocol |

- **Download the release binary file**

  Download from the [link](https://github.com/goharbor/harbor/releases)

- ``` shell
  tar -xvf {the downloaded file}
  ```

- **Configuring Harbor**

  - hostname
  - data_volume
  - harbor_admin_password
  - database
  - and so on, visit [document](https://github.com/goharbor/harbor/blob/master/docs/installation_guide.md) for more deatil

- ``` shell
  sudo ./install
  ```

- Add the hostname into your docker **insecure-registries** on your client host

- ``` shell
  # Now, you are able to execute "dockerlogin {harborhostname}" on terminal
  eg. docker login 192.168.1.155
  ```

- ``` shell
  # after those, push image to your private harbor
  docker tag SOURCE_IMAGE[:TAG] {hostname}/{projectname}/IMAGE[:TAG]
  docker push {hostname}/{projectname}/IMAGE[:TAG]
  ```

  

