## Custom busybox image with CMD[]

### Podman Build
❯ podman build custom-busybox -t docker.io/scribblepad/custom-busybox:latest

### Podman Push to docker.io
❯ podman push docker.io/scribblepad/custom-busybox

### Podman run command
❯ podman run docker.io/scribblepad/custom-busybox

RED

### Podman run command overriding the CMD

❯ podman run docker.io/scribblepad/custom-busybox echo BLUE
BLUE

