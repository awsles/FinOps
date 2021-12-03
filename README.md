# #FinOps - Cloud Financial Operations
Aside from Information Security, one of my keen areas of interest is Cloud Operations and in particular, how to use cloud effectively.
Here, I share some of my own observations and experiences in helping organizations to migrate to and use cloud more cost effectively.
This is not meant to be an exhaustive list. Rather, just a higher level overview of things you might consider in the course of your own #FinOps efforts.

# Cloud vs. On-Premise
I regularly see claims that public cloud computing is MANY times more expensive than on-premise.
Left ungoverned, this certainly will be true. And if you just consider equipment and basic expenses for compute & storage, you'll definitely draw that conclusion.

## Considerations
There are numerous factors to consider in making a *fair* cloud vs. on-premise comparision, many of which are less tangible.

Consider:
* The numerous service / maintenance contracts that add up (not to mention the pain of negotiating each time)
* All the supporting infrastructure costs (switches, routers, cabling, supporting software, etc.)
* Staff & recruiting costs (often omitted in the equations; don't forget office space cost as well)
* The business cost of *time* - How long did you have to wait for that LUN to be added to your server?
* Data Center overhead (including electricity, network redundancy, etc.)
* Business Continuity / Resiliency overhead (stand-by data centers, etc.)
* Your actual utilization of IT resources - How much are you paying just to have compute on stand-by availability?
* Are you in the business of running data centers or of providing a B2C or B2B product / service?
* And so on...

But when you add it up... and I mean really add it up, you should arrive at a different conclusion - at least in the ballpark.
Essentially, this means you have to amortize the entire cost of your compute (including the aforementioned factors) over the life of the equipment.
Even if that turns out to be moderately less expensive, is it really worth the hassle?  Is running a data center your core business?
Now factor in what your actual compute needs are (i.e., 80 cores for 14 hours / day for peak demand, and then 8 cores for non-peak). 

In doing a comparative assessment, work with your finance team to look at your actual on-premise related expenditures.
You may be surprised by the different things you are paying for. :smile:
For cloud, cost is consumption-based. You only pay for what you use while you are using it.

### Monolithic Workloads
A big challenge are older monolithic workloads, which often were built with little regard to cost of computing vs utilization.
Such workloads are designed to run 24x7, and will happily sit idle until needed.
Some applications will utilize load balancers to distribute the workload across the available servers, and to ensure overall availability.
Primarily, this is done to ensure that the applicable service remains available even if an individual server or two fails or is taken offline for maintenance.

Rarely are compute cores re-deployed for other purposes during application idle periods.
It certainly *can* be done, but requires a substantial effort to manage that re-distribution of compute.
And you may not have a need for very much compute during off hours, so all that hardware may largely sit idle anyway.

### Hybrid Cloud
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

### Get out of the Data Center Business
Are running data center's your companies core business? 
You might be tempted to ask what the difference would be with operating cloud data centers. Quite a bit actually.
ALL of that management and operational overhead is taken care of by the cloud service provider.
On top of that, an easy-to-use UI is provided which makes it easy to deploy and manage services.

### Self-Service Enablement
Provisioning accounts for a notable cost in managing on-premise IT infrastructure.
Specialized expertise is usually required to provising virtual machines and attach the storage.

By far, the biggest advantage of cloud is the instant provisioning.
In a few clicks and in less than a couple of minutes, you can deploy new compute and other services.
No ticket needed. No waiting days for someone to provision equipment.
And just as quickly, you can remove that deployment if it wasn't what you needed. 
And you only pay for that resource while it is deployed.
Guardrails can be deployed within the cloud to limit the actions that people can take (so as not to inadvertently deploy a costly content delivery network for example).

It should be note that companies such as VMWare and Snow Software are building solutions which bring self-service enablement to on-premise and even hybrid-cloud environments.
One dashboard. Multiple environments, provided that the equipment already have can be managed by that dashboard.

### Lift and Shift
One of the first ways to migrate to the cloud is "lift and shift", whereby existing applications are simply moved as-is to the cloud.
The additional cost can be considerable if performed blindly.
But cost also can be reasonable if done with a bit of care using some of the cost saving techiques further below -- and without having to rewrite your application.

### Cloud-Enable your Applications
Ideally, you'll have the luxury of re-writing your application workloads to utilize the cloud smartly
New applications should cloud-enabled from the start to only consume the cloud features that are needed. 
Developing such takes time though -- so this should be part of your longer term plans.

# Cloud Cost-Saving Techniques
There are a number of techniques for reducing cloud costs.
The general rule of thumb for cloud is that compute is expensive and storage is cheap.
So ideally, you should only use the minimal amount of compute and storage required.
But there are a number of tactics -- below are some of the most common.

### Tag Your Resources
All of your cloud deployments ideally should be tagged to identify the associated cost center, project, or similar, so that proper cross-charging can take place.
It also helps you to identify who "owns" certain resources. AWS accounts and Azure subscriptions can and *should* be used to segregate different business areas
and improve security.  Azure provides "resource groups" that should be used to group items which share the same lifecycle (i.e., all of the resources tied to a specific application deployment).

### Organize your Storage
Make sure your have a good data retention program in place, which discards data that is no longer required.
Not only is this good practice and will reduce storage costs, but in growing cases, it is also a regulatory compliance requirement.
There are simple things that can be done, such as identifying and removing duplicate data; consolidating data sources; 
purging old log files; archiving data that isn't used (but may still need to be retained for some period); etc.

### RightSizing
Figure out what your workload's compute, memory, and storage utilization are over the course of a week or month.
Generally, you'll probably observe an average compute utilization of 2 to 4 percent, with some bursts in between. 
These bursts will likely occur during business (or shopping) hours.

You might be running an application on a nice 24 core memory rich server on premise. But does the utilization justify this?
Perhaps 8 cores and half as much memory may suffice. This is a good practice even for on-premise systems.

### Poor Man's Scaling
If your workload can run on multiple compute instances with a load balancer, then do so.
With a little bit of scripting, and without rewriting your existing application, you can
monitor your application's utilization and dynamically start and stop additional instances or even resize instances as needed.
If there are peak times with unexpected bursts, your script can account for this.
If the application has counters and/or an API to monitor its health and use, even better.

If you have moved a database workload such as MS-SQL, you can dynamically resize it on the fly as well,
so that the meter rate during off hours is lower than peak hours.

Yet another technique (again with a little bit of scripting) is to have VMs shut themselves down when no longer in use.
In doing so, it it very important that the cloud API be used so that the VM is properly deallocated and not simply sitting in a "shutdown" state still being charged.
This approach might need a complementary script to start additional VMs when the demand increases.

These are some of the best techniques for lift-and-shift workloads, which don't require an application re-write.

### Scale Sets
Scale sets can also be used to manage monolithic loads which are load-balancer friendly.
These provide an effective way to keep compute costs reasonable -- but you will need to do a bit of scripting to
help identify when scale up and scale down is required.

On AWS, the scale up happens almost instantly, whereas on Azure, it takes ~2 minutes
(my guess is AWS keeps a private standby ready to run if its requested - something I was Azure would do).

### Reserved Instances
Reserved instances allow you to set aside dedicated computing at a substantially reduced cost, but it it coupled to committing to a certain period (1 to 3 years).
It is not a specific VM instance, but is generally a particular VM size or family.
Usage of VMs within that size will first be charged against at the reduced reserved instance rate, up to the committment, at which time, the charge reverts to the standard VM contract rate.
Microsoft Azure tends to be more flexible with reserved instance committments, allowing you to periodically move and resize them, and even apply the cost towards other VMs within the same family.
Amazon AWS is more strict on this, though you can pay more for more flexibility.

One key point here: DO NOT BOOK ALL YOUR RESERVED INSTANCES AT ONCE!
If you decide to move to reserved instances for certain workloads, then do so on a rolling basis... quarterly or even monthly.
The reason is that all your renewals won't all happen at the same time.
Invariably, your needs change throughout the course of the year.
If you have rolllowing reserved instance renewals, it its easier to manage and resize as you go.

### Spot Instances
Spot instances provide another low-cost computing option.
But they come with a hefty tradeoff. A spot instance can be terminated with a 2 minute notice from the cloud provider.
If your workload can handle this (and shut down or hibernate in less than 2 minutes), it may be a good cost savings tactic.
The pricing model is slightly auction-like. You 'bid' on a VM size, and you may or may not get it.
And you may lose it if you are outbid when compute resources become limited.

Spot instances can be put behind a load balancer to manage the workload accessibility, if needed.
Scripting can be used to manage the shutdown gracefully, where monolithic applications are concerned.
Another tactic is to use spot instances to scale out, while still maintaining core committed instance(s).

There are some third party tools that can manage workloads using spot instances quite effectively.

### Scheduled VMs
Another simple technique is scheduled services, where certain services automatically shut down during off hours.
While this may have limited appeal, it is an available measure.  
This can be coupled with magic links or on-demand access which start the service if someone needs it.

### Serverless
Used wisely, serverless event-driven computing can be used, such as Azure functions and AWS lambda.
These require an aqpplication re-write in most instances, but can be used to augment existing monolithic applications.

### Orphaned Resources
One of the most common mistakes in cloud computing is failing to fully delete resources.
For example, when you create a virtual machine, you will attach storage and a network interface to it.
Frequently though, people for get to delete the associated storage and network interface when they delete a VM that is no longer needed.
Thus, you continue to pay for that storage and network interface - sometimes for years before someone realizes it - and then has to run around and figure out who's storage it is.

Personally, I wrote a powershell script to identify such resources, saving one company $250,000 per year as they were no third party tools at the time that would help.

### Guardrails
Guardrails can be deployed which can limit the types and sizes of resources that a person can deploy,
as well as impose certain security configuration requirements. 
This provides a nice balance to self-service enablement. 
All of the cloud providers offer controls to manage configuration and limit spend via budgets and alerts.

### OpEx vs CapEx
A common accounting challenge is transitioning from a Capital Expenditure (CapEx) to an Operational Expenditure (OpEx) model.
CapEx allows resources to be capitalized and depreciated, usually over a 3 year period for technology, while OpEx bears the expense when it is incurred.
Each has its accounting advantages, and transitioning requires the close cooperation of the finance time.

With public cloud though, it can be capitalized with appropriate committments. Reserved instances are one means.
If you need to retain a partial CapEx model, discuss this with your cloud providers.

### Multi_Cloud
Many companies are adopting a multi-cloud strategy. 
I've often seen internal company workloads placed on Azure, customer-facing workloads placed on AWS, and data science workloads on GCP.
MongoDB Atlas, Oracle cloud, and Snowflake are also becoming popular cloud-to-cloud and cloud-to-on-premise services.

At retail Pay-as-you-go,all of the providers tend to hover within pennies of one another, so you need to choose based on your workload needs and other criteria.
In my own experience and analysis, I have found that Microsoft Azure tends to be less expensive than Amazon AWS under contract. But your mileage may vary.

Azure provides an excellent user interface with great insights and fine grained control. AWS, on the other hand, tends to be slightly less granular and slightly less intuitive (it feels like an early 2000's web UI). Linux fans tend to gravitate to AWS for this reason. I also find Azure APIs to be more exhaustive and well throught out.
For example, in Azure you can enumerate all of your resources across all subscriptions in a tenant using a single API call.  In AWS, you have to either examine the bill or call each of the 180+ service APIs, inquiring about resources (amazing fact!).

GCP takes a project-based approach, with a UI that (in my experience) is slightly challenging in the way the resources are display.
Otherwise though, I found navigation to be easy. My familiarity beyond that is limited.

### Managed Service Providers
A good managed service provider (MSP) can help you on your cloud journey and help you manage costs.
They can provide guidance, help with guardrails and self-service enablement, move workloads, help identify cost saving opportunities, and operate product services on your behalf.

However, I would not recommend using an MSP to perform deployments on behalf of developers (i.e., ticket-based IT).
First, it introduces an unnecessary time lag (more ticket-based IT), which slows down development.
Second, if a change is needed, it means another ticket, and more time.
Third, it treats developers as untrusted to properly provision cloud services.
Fourth, MSPs will often have a nominal "charge" to do deployments. That adds up.
Lastly, it doesn't make sense to pay someone else to click the same easy buttons that a developer could click. 

So enable self-service where it makes sense to do so. Use MSPs as needed to help accelerate your cloud transformation and guide your #FinOps journey.

---
# Resources

* https://azure.microsoft.com/en-us/overview/cost-optimization/
* https://aws.amazon.com/aws-cost-management/aws-cost-optimization/
* https://cloud.google.com/cost-management
* https://www.oracle.com/webfolder/s/quicktours/scm/gqt-scm-manuf-costing-overview/index.html


