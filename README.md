# Rootless podman and slirp4netns slow performance with NGINX (~5 second reponse) [#20465](https://github.com/containers/podman/issues/20465)

### Issue Description

NGINX has poor performance when running under rootless podman and slirp4netns

Lowering the MTU to 1500 from the podman default of 65520 with `--network slirp4netns:mtu=1500` fixes the issue. Strangely, after the container is ran  once with the `--network slirp4netns:mtu=1500` option, NGINX container works fine even with the option removed.

See [#6945](https://github.com/containers/podman/issues/6945) for a related issue.

### Steps to reproduce the issue

```
 git clone https://github.com/arbrsts/vite-react-nginx-slow-load-reproducible-example
 podman build ./nginx/. -t slow-load
 podman run -p 4000:4000 slow-load
 npm i
 npm run dev
```
