# Demo of Kubernetes Features for P47

## TODO

- make a basic slide of a kubernetes cluster

## Landing Page
https://pollux.diamond.ac.uk/

This is where developers and systems managers come to monitor and control services running in the cluster.

Pollux is our staging cluster where we test features that are going to be rolled into our central cluster called Argus. We share this cluster among a number of test beamlines. Production beamlines will each get there own dedicated cluster at DLS.

The tools available from here are all widely available FOSS that our cluster adminstrators provide on every cluster at DLS.

These are:

- Dashboard: the standard Kubernetes Dashboard for monitoring and controlling K8S resources
- KeyCloak: our single sign on shared authetication service
- Prometheus: montitoring and time series database
- Grafana: an open observability platform to visualize the data from Prometheus and other sources
- Alertmanager: for notifying when prometheus monitor limits are exceeded
- Stackrox: security dashboard - monitors and alerts on CVEs (Common Vulnerabilities and Exposures).

## Stackrox

This tool monitors the containers that are currently running in the cluster and checks them for potential vunerabilities.

It turns out that the ioc-adaravis container has a few CVE's in it and is sitting high in the list of issues on the whole cluster.

Let's drill in to this. There is only one issue that is flagged as 'important' that is https://pollux-stackrox.diamond.ac.uk/main/vulnerability-management/image/sha256:f0d5a071b463c2c23d4f6dd59f3659691db6688d3f9b24d8edf00ca87c3c44be?workflowState[0][t]=IMAGE_CVE&workflowState[0][i]=CVE-2024-22190%23ubuntu%3A22.04.

It's CVE-2024-22190 and it turns out that this only affects windows so we could dismiss this issue. Also note that this is an old version of ioc-adaravis running on one of the other test beamlines that has not been updated. The newer version is much more streamlined and does not use the package gitpython from which the vunerabiltiy arises.

## Alert Manager

TODO: need to understand this one.

## Grafana

TODO: do we have a Channel access plugin?

Prometheus collects a great deal of information on the state of all of the resources in the cluster and stores them in a time series database. Gafana let's us visualize that data.

Here for example is the node information for the single server that is running all of the p47 services. https://pollux-grafana.diamond.ac.uk/d/ddqqfifujqgaoe/node-exporter-nodes?orgId=1&refresh=30s&var-datasource=default&var-cluster=&var-instance=172.23.242.47:9100

You can see when new container images were pulled into the node and there was significant network activity.

If you want more you can go to the full node exporter which has more details than I know what to do with.

# Argo CD and 'ec'

For a more application centric view of the cluster we have the GUI of the Contiuous Deployment tool Argo CD. see https://argocd.diamond.ac.uk/applications?showFavorites=false&proj=p47-beamline

TODO get ec up and running with Argo Back end.

