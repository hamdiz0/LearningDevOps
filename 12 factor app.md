# 12 FACTOR APP

<img src="z-imgs/12 factors.jpg" style="width:100%">

## `1-Codebase` : 

* Use one codebase in version control, deploying it to different environments.

## `2-Dependencies` :

* Explicitly declare all dependencies, keeping them isolated for consistency.

## `3-Config` : 

* Store configurations in environment variables, not in the codebase.

## `4-Backing Services` : 

* Treat external services (like databases) as easily replaceable resources.

## `5-Build, Release, Run` :

* Separate building, releasing, and running to ensure controlled deployments.

## `6-Processes` :

* Run the app as stateless processes; use external storage for data.

## `7-Port Binding` :

* Bind the app to a port, so it’s accessible as a service.

## `8-Concurrency` :

* Scale by running multiple instances of processes.

## `9-Disposability` :

* Make processes start and stop quickly to aid scalability.

## `10-Dev/prod Parity` :

* Keep development and production environments similar.

## `11-Logs` :

* Treat logs as event streams, accessible for monitoring.

## `12-Admin Processes` :

* Run admin tasks (e.g., database updates) separately from the main app.
