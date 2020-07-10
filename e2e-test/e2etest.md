# Kubernetes end-to-end-tests
so how to be sure for every PR no breaking changes and no fault happens.
Kubernetes uses `e2e-test` which is written with Ginkgo and we locally can test e2e tests with setting up a Kubernetes cluster in docker with [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/). so for every e2e tests we can setup a Kubernetes clsuter and run our tests. [a good source for giving you a view](https://www.youtube.com/watch?v=8KtmevMFfxA)
