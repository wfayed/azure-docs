---
 title: include file
 description: include file
 services: virtual-machines
 author: jonbeck7
 ms.service: virtual-machines
 ms.topic: include
 ms.date: 05/29/2018
 ms.author: azcspmt;jonbeck;cynthn;danlep
 ms.custom: include file
---

## Deployment considerations
* **Azure subscription** – To deploy more than a few compute-intensive instances, consider a pay-as-you-go subscription or other purchase options. If you're using an [Azure free account](https://azure.microsoft.com/free/), you can use only a limited number of Azure compute cores.

* **Pricing and availability** - These VM sizes are offered only in the Standard pricing tier. Check [Products available by region]
(https://azure.microsoft.com/regions/services/) for availability in Azure regions. 
* **Cores quota** – You might need to increase the cores quota in your Azure subscription from the default value. Your subscription might also limit the number of cores you can deploy in certain VM size families, including the H-series. To request a quota increase, [open an online customer support request](../articles/azure-supportability/how-to-create-azure-support-request.md) at no charge. (Default limits may vary depending on your subscription category.)
  
  > [!NOTE]
  > Contact Azure Support if you have large-scale capacity needs. Azure quotas are credit limits, not capacity guarantees. Regardless of your quota, you are only charged for cores that you use.
  > 
  > 
* **Virtual network** – An Azure [virtual network](https://azure.microsoft.com/documentation/services/virtual-network/) is not required to use the compute-intensive instances. However, for many deployments you need at least a cloud-based Azure virtual network, or a site-to-site connection if you need to access on-premises resources. When needed, create a new virtual network to deploy the instances. Adding compute-intensive VMs to a virtual network in an affinity group is not supported.
* **Resizing** – Because of their specialized hardware, you can only resize compute-intensive instances within the same size family (H-series or compute-intensive A-series). For example, you can only resize an H-series VM from one H-series size to another. In addition, resizing from a non-compute-intensive size to a compute-intensive size is not supported.  

## RDMA-capable instances
A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity. (Selected N-series sizes designated with 'r' such as NC24r are also RDMA-capable.) This interface is in addition to the standard Azure network interface available to other VM sizes. 
  
This interface allows the RDMA-capable instances to communicate over an InfiniBand (IB) network, operating at FDR rates for H16r, H16mr, and RDMA-capable N-series virtual machines, and QDR rates for A8 and A9 virtual machines. These RDMA capabilities can boost the scalability and performance of certain Message Passing Interface (MPI) applications.

> [!NOTE]
> In Azure, IP over IB is not supported. Only RDMA over IB is supported.
>

Deploy the RDMA-capable HPC VMs in the same availability set or VM scale set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model). If you use a VM scale set, ensure that you limit the deployment to a single placement group; for example, in a Resource Manager template, set the *singlePlacementGroup* property to *true*. Additional requirements for RDMA-capable HPC VMs to access the Azure RDMA network follow.