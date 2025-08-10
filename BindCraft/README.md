# BindCraft (ver. 1.5.2)

※ In the code blocks, `🍅` indicates a command prompt.

## Building the Container

```bash
# Build the container based on the .def file
🍅 apptainer build ./bindcraft-v1.5.2.sif ./def_file/bindcraft-v1.5.2.def
```

## Example Shell Script to Run the Container

```bash
#!/usr/bin/env bash
set -eo pipefail

APPTAINER_IMAGE="/mnt/d/apptainer_image"
function bindcraft-app() {
  apptainer run \
    --nvccli \
    --bind /mnt/d \
    --net --network none \
    ${APPTAINER_IMAGE}/bindcraft-v1.5.2.sif "$@"
}

BINDCRAFT_HOME="/usr/local/apps/BindCraft"
bindcraft-app python3 -u -m bindcraft \
  --settings ./settings_target/PDL1.json \
  --filters ${BINDCRAFT_HOME}/settings_filters/default_filters.json \
  --advanced ${BINDCRAFT_HOME}/settings_advanced/default_4stage_multimer.json
```
