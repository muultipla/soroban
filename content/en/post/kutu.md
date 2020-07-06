{
   "date": "2020-06-12",
   "title": "Kutu, K8s useful tools updater",
   "weight": 10,
   "image": "kutu.png",
   "authors": [ "mcabrerizo" ],
   "branches": [ "tech" ],
   "tags": [ "dev", "kubernetes", "cli", "utils" ]
}

Here in **Muultipla** we love Kubernetes, and we love tools like kubectl, minikube, skaffold and kustomize.

Some of us use Linux and we like to download the latest version of those tools from their GitHub repositories releases pages. 

Those tools change frequently so we've created a simple binary written in Go that checks if those tools are outdated and update them if needed. Sure, you have other ways like using **brew** but we like to develop our own stuff and it runs nicely.

This tool is called Kutu (K8s useful tools updater) and you can visit [our repository in Github](https://github.com/muultipla/kutu) if you want to try our [pre-release binaries for Linux and Mac](https://github.com/muultipla/kutu/releases). Comments are welcomed.

Thanks!
