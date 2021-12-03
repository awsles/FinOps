# #FinOps - Cloud Financial Operations
Aside from Information Security, one of my keen areas of interest is Cloud Operations and in particular, how to use cloud effectively.
Here, I share some of my own observations and experiences in helping organizations to migrate to and use cloud more effectively.
This is not meant to be an exhaustive list. Rather, just a higher level overview of things you might consider in the course of your own #FinOps efforts.

DRAFT

# Cloud vs. On-Premise
I regularly see claims that public cloud computing is MANY times more expensive than on-premise.
Left ungoverned, this certainly will be true. And if you just consider equipment and basic expenses for compute & storage, you'll definitely draw that conclusion.
There are numerous factors to consider in making a *fair* cloud vs. on-premise comparision, many of which are less tangible.

Consider:
* All those vendor service / maintenance contracts that add up
* All the supporting infrastructure costs (switches, routers, cabling, supporting software, etc.)
* Staff & recruiting costs (often omitted in the equations; don't forget office space cost)
* The business cost of *time* - How long did you have to wait for that LUN to be added to your server?
* Business Continuity / Resiliency overhead (stand-by data centers, etc.)
* Data Center costs (including electricity, network redundancy, etc.)
* Actual utilization of on-premise storage & compute - How much are you paying just to have compute on stand-by avialability?
* Are you in the business of running data centers or of providing a B2C or B2B product / service?
* And so on...

But when you add it up... and I mean really add it up, you should arrive at a different conclusion - at least in the ballpark.
Essentially, this means you have to amortize the entire cost of your compute (including the aforementioned factors) over the life of the equipment.
Even if that turns out to be moderately less expensive, is it really worth the hassle?  Is running a data center your core business?
Now factor in what your actual compute needs are (i.e., 80 cores for 14 hours / day for peak demand, and then 8 cores for non-peak). 

## Monolithic Workloads
A big challenge are older monolithic workloads, which often were built with little regard to cost of computing vs utilization.
Such workloads are designed to run 24x7, and will happily sit idle until needed.
Some applications will utilize load balancers to distribute the workload across the available servers, and to ensure overall availability.
Primarily, this is done to ensure that the applicable service remains available even if an individual server or two fails or is taken offline for maintenance.

Rarely are compute cores re-deployed for other purposes during application idle periods.
It certainly *can* be done, but requires a substantial effort to manage that re-distribution of compute.
And you may not have a need for very much compute during off hours, so all that hardware may largely sit idle anyway.

## Hybrid
There are cases where on-premise should be used.
The CIO of McDonald's Spain pointed out that critically, each of their stores needs to have its own local compute so that the store can operate even if the internet is down.
Similarly, consider a warehouse operation.  Local IT infrastructure would be used for automation management, capturing of IoT data, etc.
In these cases, having a (suitably sized) on-premise footprint centainly makes sense.
The back-end services which aggregate data and perform other functions, however, can (and probably should be) be cloud-based.

So what about having your own data center? Well, you'll probably need two if you have a high availability requirement (in case one DC fails).
If you legitimately run 24x7x365 at scale with few idle periods, then it might make sense to run your own infrastructure (think Facebook).
Index companies such as S&P Global and Dow Jones need to run compute-intensive simulations, often requiring thousands of cores - but only for short bursts of time.
If they operate a rotational simulations schedule, they may be able to keep their on-premise compute infrastructure heavily utilized over each 24 hour period,
and therefore justify operating on-premise.

But most businesses have peaks and valleys in their compute needs, with little to do during idle periods.  
Why pay of that idle compute time?


# Migrating to the Cloud
How do do you migrate to the cloud while reasonably managing costs?
During any data center migration, there is usually an overlap where you are paying for both services at the same time.
This holds true for cloud as well. 

## Get out of the Data Center Business
Are running data center's your companies core business? 
You might be tempted to ask what the difference would be with operating cloud data centers. Quite a bit actually.
ALL of that management and operational overhead is taken care of by the cloud service provider.
On top of that, an easy-to-use UI is provided which makes it easy to deploy and manage services.

## Self-Service Enablement
Provisioning accounts for a notable cost in managing on-premise IT infrastructure.
Specialized expertise is usually required to provising virtual machines and attach the storage.

By far, the biggest advantage of cloud is the instant provisioning.
In a few clicks and in less than a couple of minutes, you can deploy new compute and other services.
No ticket needed. No waiting days for someone to provision equipment.
And just as quickly, you can remove that deployment if it wasn't what you needed. 
And you only pay for that resource while it is deployed.

It should be note that companies such as VMWare and Snow Software are building solutions which bring self-service enablement to on-premise and even hybrid-cloud environments.
One dashboard. Multiple environments. That is compelling -- if the equipment you've chosen to purchase can be managed by that dashboard (including the older stuff).

## Build & Tear down felxibility

## Lift and Shift

## Re-Write

## Orphaned Resources

## Guardrails

## Reserved Instances

## Spot Instances

## Functions

## Poor Man's Scaling
Use a load balancer
Size up / size down VMs dynamically
Use SCale Sets






## OpEx vs CapEx



consumption-based



how much are you actually utilizing your on-prem compute?, and so on.



The general rule of thumb for cloud is that compute is expensive and storage is cheap.



## Self-Service Enablement



Even for the aforementioned index companies, is it really worth the hassle to manage on-premise data centers?
 

That said, it is NOT easy... especially for traditional server-based work-loads. The savings won't happen overnight, but you can make it reasonable and sometimes, even cheaper, so that your business can focus on its own core competencies (is really running a data center increase your sales?). #FinOps #CloudComputing

TIP: When doing an assessment, get the list of outgoing figures from the finance folks.

## Which Cloud Provider?

