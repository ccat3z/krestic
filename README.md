# Krestic

Backup a pvc using restic in kubernetes.

## Environments

* `KRESTIC_POD_NAME`: (Optional) Pod name of krestic it self.
* `KRESTIC_PVC_NAME`: (Optional if `KRESTIC_POD_NAME` is specified)
   Target backup persistent volume claims.

## Hooks

You can specify one or more commands to execute in a container in a pod before
or after performing a backup task. You can specify hooks on a pod by labels 
and annotations.

### Pod Labels

* `krestic.ccat3z.github.io/hooks: false`. Enable hooks, default is `false`.

### Pod Annotations

* `krestic.ccat3z.github.io/hooks`. Define hooks.

  ``` yaml
  krestic.ccat3z.github.io/hooks:
    - type: pre  # or post
      # The first container will be used if it is empty.
      container:
      # The command to execute.
      command: []
      # The hook will only be executed when these volumes are backuped.
      # If `volumes` is empty list, all persistent volume claims will be matched.
      volumes: []
  ```