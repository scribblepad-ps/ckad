# ENV SETUP
## alias kc=kubectl
## export dr=--dry-run=client -o yaml 
## set -gx  dr --dry-run=client -o yaml
## alias kns="kc config set-context --current --namespace"
set -gx now "--grace-period=0 --force"
