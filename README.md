**WARNING:** This is a dysfunctional repository with the purpose of serving as a training exercise.


# TAP Angular Example

## Prerequisites

TAP 1.1 (Tanzu Application Platform) ships with TBS (Tanzu Build Service) which
is based on kpack. TBS brings a bunch of `ClusterBuilders` none of which
include the `nodejs` and `nginx` buildpack in the same `Group`. Therefore,
building and Angular app that is served as static files via Nginx is not
possible with the default configuration.

Luckily, TAP is very extensible and customizable so that we can make this work
with only a few tweaks.

1. Create `ClusterBuilder` that includes the `web-servers` buildpack
```
REGISTY="gcr.io/cso-pcfs-emea-mewald"
kp clusterstore create spa \
  -b paketobuildpacks/web-servers

kp clusterbuilder create spa \
  --buildpack paketo-buildpacks/web-servers \
  --tag $REGISTRY/spa:v2 \
  --stack full \
  --store spa
```

## Task
Find out a way to use that newly created `ClusterBuilder` for this app

