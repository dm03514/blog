# Debubbing DevOps: Local Deploy Visibility

Local Deploys, an action item always pushed to the end of the backlog.  We know we shouldn't be performing actions locally but since they aren't resulting in errors or huge incidents addressing it often pushed off.  At ValueStream, we beleive the first step to making sustainable changes to any system is understanding how the __ and connections.  This post shows how ValueStream can be used to start monitoring local actions with very low effort.  This allows organizations to treat these important local actions as the first class citizens they are, monitor their performance and build an inventory of locally executed operations.


## Problem

Local deploys are common place in many startups.  Processes that start on small teams that don't want to invest in cloud deployments are inherted as companies scales.  Because of this there may be some critical production tasks that.

Here at ValueStream we deploy to production locally using google cloud SDK

Flat events are not sufficient in order to form a systems view of any domain.


## Record The Local Deploy

This happens at the event level.

## Record the trace

ValueStream


## Example

This post illustrates how ValueStream can be used to monitor local depoloys using ValueStream's own production deployment process as an example.  For background ValueStream is hosted in Google Cloud and uses Goolge App engine to host its production infrasturucture.  The deployment process is executed daily and requires the following steps:

- Builds a [Docker Image](https://docs.docker.com/v17.09/engine/userguide/storagedriver/imagesandcontainers/#images-and-layers)
- Pushes to [Google Container Registry](https://cloud.google.com/container-registry/)
- Issues a deploy using `gcloud` tool

A simple bash script is used to accomplish this:

```
# deploy-api.sh

docker build -f Dockerfile.api -t valuestream-api .

docker tag valuestream-api us.gcr.io/value-stream/valuestream-api
docker push us.gcr.io/value-stream/valuestream-api

gcloud app deploy \
    --image-url us.gcr.io/value-stream/valuestream-api devops/gae/app.api.yaml \
    --version=v1 \
    --quiet
```

While this is easy there's no visibility audit log or history.  We deploy 1-2 times a day, is this a good candidate to improve? How long are we spending in the deploy? What's the success rate? Basically as it stands now there's no visibility or answers to these common DevOps and delivery questions.

```
TRACEID="$(vscli event -tag='source|gcloud' -tag='service|api' -type=pipeline start)"

...

vscli event -type=pipeline end -event-id=${TRACEID}
```

(Images Below shows Traces in LightStep; ValueStream OSS can output to Jaeger and LightStep, and ValueStream cloud beta will only ship to LightStep, requiring a free LightStep account to use LINK):


----


While extremely useful for debugging DevOps, ValueStream's real power comes from being able to model processes.  The deployment script has 3 different logical steps:
- Build 
- Push
- Deploy

ValueStream is intelligentlly able to connect these.  Using the `vscli` tool to do this looks like:

```

```

Many tools naturally have this format, where work is in many different states, and the duration of each state is important:

- JIRA story moving across swimlanes
- Build Pipelines, Jenkins, Gitlab, Local, etc
- Team Working on multiple issues or repos towards completeing an Epic 

Modeling this as a pipeline 
Combined with LightStep can be used to intellegintly debug delivery across multiple different tools, teams, or processes LINK.

This allows you to filtered for commonly errored or latent transactions and then instantly have context on why, are there shared technologies?
kIs it a teamt raining issue? 

### Local Actions
- SELECT Events where source="local" GROUP BY Event. Action;

### Performance by action
- SELECT Events where source="local" GROUP BY Event. Action;

### Sources
- SELECT Events where source="local" GROUP BY Event. Action;

### Traces

