# Purpose of this Folder

This folder should contain the solution to the exercise. This would be added to a concept walking through the solution with the student for this exercise.
# 4.15 Exercise: Define Operational Test Plan for Hardening
### In what environment(s) will the change be tested?
* Test should happen in a non-productive environment
* e.g. develop or staging
* Metrics can be monitored using observability and monitoring techniques like Prometheus and Grafana.

### Can the change be canary tested with some traffic directed to simulate load?
* Of course. This is a good idea since some issues only appear under load
* E.g. via a load balancer configuration

### Does the environment mimic production?
* Yes. The non-productive environment should be representative of the production

### Can the change be rolled out incrementally?
* Yes. This means that productive operation does not have to be interrupted.

### Can the change be safely rolled back?
* To be able to rollback metrics for regressions should closely be monitored, i.e. undesired changes or consequences from hardening.
* Editing the cluster.yaml should be version-controlled with Git so the change can be rolled back.