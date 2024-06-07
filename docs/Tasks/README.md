# Overview
* Task 
  * TODO:
  * vs `ClusterTask`
    * availability
      * Task is available within 1! specific namespace
      * ClusterTask is available across ENTIRE cluster
- [Examples](https://github.com/tektoncd/catalog/tree/main/task)
- TODO:

# Configuring a Task
- TODO:
## Emitting `Results`
* uses
  * being viewed by users
  * consumed by other [Tasks](https://tekton.dev/docs/pipelines/pipelines/#passing-one-tasks-results-into-the-parameters-or-when-expressions-of-another) or [Pipelines](https://tekton.dev/docs/pipelines/pipelines/#emitting-results-from-a-pipeline)
  * hold small amounts of data
    * _Example:_ commitSHA, branch name, ephemeral namespaces, ...
* [Task.spec.results](https://tekton.dev/docs/pipelines/pipeline-api/#tekton.dev/v1beta1.Task)
  * way to declare the task's results
* variables about results available
  * `results.<resultName>.path` / `results['<resultName>'].path` / `results["<resultName>"].path` 
    * path where Tekton stores result's data
* NO processing by Tekton on the result's content!!
* _Examples:_
  * Create a task
    * `kubectl apply -f emittingresults_task.yaml`
  * Create a taskRun
    * `kubectl apply -f emittingresults_taskrun.yaml`
  * Check the results
    * `kubectl describe taskrun/taskrun-param-enum` & check in 'status.results'
    * `kubectl get pods` & check the podName & `kubectl describe pod/podName` & check in 'containers.i.State.Message'
* TODO:
## Variable substitution
* [Available task variables](https://github.com/tektoncd/pipeline/blob/main/docs/variables.md#variables-available-in-a-task)
- TODO:

# Notes
## Prerequisites to run examples
* Run some docker daemon
  * [Docker desktop](https://www.docker.com/products/docker-desktop/)
  * [Rancher dektop](https://rancherdesktop.io/)
* Install some local cluster
  * [minikube](https://minikube.sigs.k8s.io/docs/start/)
  * [kind](https://kind.sigs.k8s.io/)
* Install [Go](https://go.dev/doc/install) & `go install sigs.k8s.io/kind@v0.19.0`
* Install Tekton Pipelines
  * `kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml`