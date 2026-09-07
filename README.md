# fabiang/nsis

Docker image for Nullsoft NSIS. NSIS let's you create Windows installers.

[![fabiang/nsis](https://img.shields.io/docker/pulls/fabiang/nsis.svg)](https://hub.docker.com/r/fabiang/nsis)
[![fabiang/nsis](https://img.shields.io/badge/License-BSD_2--Clause-orange.svg)](https://github.com/fabiang/docker-nsis)
[![Docker Image](https://github.com/fabiang/docker-nsis/actions/workflows/docker.yml/badge.svg)](https://github.com/fabiang/docker-nsis/actions/workflows/docker.yml)

## Available tags

* 3.12-windowsservercore-ltsc2022, 3-windowsservercore-ltsc2022
* 3.12-windowsservercore-ltsc2025, 3-windowsservercore-ltsc2025
* 3.12-alpine, 3-alpine

## Usage

```bash
  docker run -it --rm \
    -v ".:/installer" \
    -w "/installer" \
    fabiang/nsis:3-alpine \
    makensis -D PRODUCT_VERSION=1.2.3 myproject.nsi
```

## License

[BSD 2-Clause License](LICENSE).
