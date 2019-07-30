# DevOps: Containers: Velocity Through Reduced Coordination

Containers have a profound impact on software organizational structure by providing a primitive which enables feature teams to fully control their system as well as application level dependencies.  Containers decouple development and operations using a common interface, which can increase velocity by reducing the amount of external coordination required to deliver software.

There are many amazing technical overviews on what [containers are](https://www.freecodecamp.org/news/demystifying-containers-101-a-deep-dive-into-container-technology-for-beginners-d7b60d8511c1/) and how to [use and production-ize them](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/).  This post focuses on how containers shift the organizational structure and the shift's affect on velocity of delivery. This post assumes knowledge of docker containers and high level knowledge of a Platform or Container Orchestrator (kubernetes, openshift, heroku, etc).

## Decoupling Operations and Development

In many traditional (pre-container) organizations operations (ops) is responsible for both infrastructure (networking, storage, provisioning, etc) and system level resources (filesystem, system libraries such as runtime versions, operating system versions, Shown below on left).  

<p align="center">
  <img src="static/infra_traditional_vs_containers_layers.png">
</p>

Containers shift this by enabling development (dev) to control [system level dependencies](https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b/#container_) (shown on right in above image). The core benefit of containers comes from shifts development one level down the level of software abstraction.  Services naturally couple Applications and system dependencies.  Containers couple these together into a single artifact.


In addition, containers also introduce a new layer of abstraction inserting a new layer the runtime/orchestrator/ or platform between the infrastructure and the system.  This acts as an interface (in the [traditional software sense](https://en.wikipedia.org/wiki/Interface_(computing)#Software_interfaces) that  decouples the dev and ops.

<p align="center">
  <img src="static/platform_layer_and_decoupling.png">
</p>

This interface general exposes configuration around cpu memory, environment around number and type , web vs asynchronous queue baes (worker)z of application instance.  Combined with the container primitive which supports controlling application and surface stem leve deenedencirs, these provide
 developers everything they need to ship the majority of features without synchronizing with  ops.  Containers redraw the traditional dependency lines


This simple change has the affect of decoupling operations and development from each deploy, enabling developers to own configuration, system libraries, application, and application configuration:

<p align="center">
  <img src="static/infra_vs_devops_deploy.png">
</p>

Containers increase velocity by reducing the number of times teams need to coordinate externally in order to deliver software.


## Development/Deployment Overhead

Since services have a naturally strict coupling between applications and the systems they run on, traditional dev and ops models (pre containers) require much cross-team coordination in order to successfully deliver software.  Configuration management is usually the highest risk, most executed, and most poorly tested, which results in long feedback loops on infrastructure changes.

The traditional (pre-container) dev and ops relationshipt Ccreates a sequence diagrams where the feature team must synchronize with the operations team, which has a significant negative impact on throughput.  The same synchronization is often required during incidents, which leads to the inverse affect on MTTR, prolonging application service outages and degradation. An example of this is shown in the sequence diagram below.  Traditional (pre-container) software deployment request development to coordinate and work with operations in order to deliver software:

<p align="center">
  <img src="static/traditional_sequence.png">
</p>

In many cases containerized model removes the need for developers to coordinate with operations

<p align="center">
  <img src="static/container_sequence.png">
</p>


Separate team is involved with value delivery , involving synchronization and organizational hops.  These teams service multiple development teams and often have their own [queue](https://medium.com/hackernoon/why-capacity-planning-needs-queueing-theory-without-the-hard-math-342a851e215c) of work taking hours or days, or potentially longer.


Another way to see the affect of containers is to visualize where a team is spending its time during feature delivery.  The gantt chart below shows a hypothetical example of a feature in a pre-container organization, that requires system or configuration related changes:

<p align="center">
  <img src="static/pre_container_delivery.png">
</p>

In this example the overhead is roughly ~30%.  This may seem a lot but I have repeatedly found real life overheads to be around this amount.  In a containerized world where dev is decoupled from ops and no coordination with ops is not required shows this reduction:

<p align="center">
  <img src="static/container_delivery_gantt.png">
</p>

While these examples only focus on delivery there are many similar benefits come from ____.  These hand offs create a nightmare for delivery accounting, is the feature done when it's handed off? Many organizations have such long deployment loops stories are marked as DONE when they are merged into master and not when they are built and deployed.
Feature Deployment.

In order to model the affect that containerization may have on delivery velocity it's important to [understand what percentage of deployments require cross team (dev & ops) coordination, and how long is spent performing that coordination](https://medium.com/@dm03514/valuestream-devops-metrics-observing-delivery-across-multiple-systems-7ae76a6e8deb).   

---

I hope this post shows how containers redefine the traditional responsibilities of both dev and ops.  By providing a primitive to development which cleanly couples application and system dependencies, containers are able to establish a clean interface between development and operations which removes the need for coordination and greatly increase delivery throughput.  Developing an understanding of the rate of coordination and its affect on delivery times is critical to modeling the affect that containers may have on an organization.  It's exciting to open a project and see that Dockerfile is present with an orchestrator manifest (heroku.yml, kubernetes config), knowing that development is empowered to autonomously configure their application, system resources and system deployment.  The [State of DevOps report](http://services.google.com/fh/files/misc/state-of-devops-2018.pdf) shows that companies that have this technical capability regularly outperform their competitors in deployment frequency and lead time.


### Resources
- https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/
- https://www.freecodecamp.org/news/demystifying-containers-101-a-deep-dive-into-container-technology-for-beginners-d7b60d8511c1/
- https://medium.com/dm03514-tech-blog/debugging-devops-using-valuestream-and-lightstep-e1f8e07f4eab
- https://en.wikipedia.org/wiki/Interface_(computing)#Software_interfaces
- https://medium.com/@dm03514/valuestream-devops-metrics-observing-delivery-across-multiple-systems-7ae76a6e8deb
- https://medium.com/hackernoon/why-capacity-planning-needs-queueing-theory-without-the-hard-math-342a851e215c
