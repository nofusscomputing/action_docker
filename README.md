## No Fuss Computing - GH Action / Workflow for docker

using the workflow requires a file be created at path `.github/workflow/docker.yaml`

``` yaml

---

name: 'CI'


on:
  push:
    branches:
      - '**'
    tags:
      - '*'


jobs:


  docker:
    if:
      (${{
        github.event.push
          ||
        github.ref_type == 'tag'
      }})
    name: 'Docker'

    uses: nofusscomputing/action_docker/.github/workflows/docker.yaml@development
    with:
      DOCKER_BUILD_IMAGE_NAME: "${{ github.repository }}"
      DOCKER_PUBLISH_REGISTRY: "ghcr.io"
      DOCKER_PUBLISH_IMAGE_NAME: "nofusscomputing/image-publish"
    secrets:
      DOCKER_PUBLISH_USERNAME: ${{ github.actor }}
      DOCKER_PUBLISH_PASSWORD: ${{ secrets.GITHUB_TOKEN }}

```
