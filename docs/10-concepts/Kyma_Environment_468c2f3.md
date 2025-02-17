<!-- loio468c2f3c3ca24c2c8497ef9f83154c44 -->

# Kyma Environment

Kyma environment provides a fully managed Kubernetes runtime based on the open-source project "Kyma". This cloud-native solution allows developers to extend SAP solutions with serverless Functions and combine them with containerized microservices.

The offered functionality ensures smooth consumption of SAP and non-SAP applications, running workloads in a highly scalable environment, and building event-based and API-based extensions.

Every Kyma environment consists of:

-   A Kubernetes cluster provisioned through project "Gardener" on a cloud provider and region \(data center\) of your choice. To find out the available regions and providers, see [Regions for the Kyma Environment](Regions_350356d.md#loio557ec3adc3174ed4914ec9d6d13487cf).
-   The open-source project ["Kyma"](https://kyma-project.io/) installed in its latest version on the provisioned cluster.

Every Kyma environment runs on a single Kubernetes cluster created for a specific subaccount. However, the configuration of the Kyma environment allows you to connect it to a multitude of SAP systems. This way, you can build various formations that aggregate the SAP systems and environment according to your business use cases.

SAP systems connected to a Kyma environment expose APIs and events collected under the Service Catalog. To extend the existing logic of these SAP services, you can build serverless applications called Functions, and trigger them to react to particular events or calls to your application's API. You can also use the Kyma environment to deploy microservices or even build full-stack applications.

For all functionalities that the Kyma environment offers, see the official [project "Kyma" documentation](https://kyma-project.io/docs/).

**Related Information**  


[Getting Started in the Kyma Environment](../20-getting-started/Getting_Started_in_the_Kyma_Environment_d1abd18.md "The getting started document describes the full list of steps you must complete as an administrator to set up a fully operational Kyma environment to which you can connect the chosen SAP solutions.")

[Development in the Kyma Environment](../30-development/Development_in_the_Kyma_Environment_606ec61.md "Learn more about developing applications in the Kyma environment.")

[Administration and Operations in the Kyma Environment](../50-administration-and-ops/Administration_and_Operations_in_the_Kyma_Environment_b8e1686.md "This is the managed offering of Kyma, which gives you a managed Kubernetes cluster with SAP BTP, Kyma runtime (based on the open-source project &quot;Kyma&quot;). The administrators of the Kyma environment take care of setting it up and make sure it is ready for developers to work with. Enable Kyma to build applications and extensions to SAP and third-party solutions, manage roles, have your Kubernetes objects backed up, and view metrics and logs.")

[Security in the Kyma Environment](../60-security/Security_in_the_Kyma_Environment_ee08fdf.md "The Kyma environment-specific security aspects include guidelines on personal data protection and details on processing and storing logs.")

 <a name="loio4a0dd09368ce40bfa3c99cae46de49e1"/>

<!-- loio4a0dd09368ce40bfa3c99cae46de49e1 -->

## Basic Concepts



This table explains basic concepts relating to the Kyma environment. It aims to give you an understanding of the Kyma environment before you actually start using it to build extensions for your SAP solutions.

> ### Note:  
> For an overview of the basic Kubernetes concepts that the Kyma environment heavily relies on, see the official [Kubernetes documentation](https://kubernetes.io/docs/reference/glossary/?all=true).




<table>
<tr>
<th valign="top">

Concept



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

Kyma cluster



</td>
<td valign="top">

A Kubernetes cluster provisioned with the latest version of the open-source project "Kyma." You can enable such a cluster on a given subaccount through the SAP BTP cockpit. After you select *Enable Kyma* on your subaccount, the cluster is provisioned automatically through Gardener on your chosen cloud service provider. To access the cluster, you must have appropriate roles assigned to your subaccount.



</td>
</tr>
<tr>
<td valign="top">

Role



</td>
<td valign="top">

Access to every cluster is managed by one of the two predefined roles assigned to a subaccount \(KymaRuntimeNamespaceAdmins or KymaRuntimeDeveloper\). These roles give the assigned users a different level of permissions suitable for different purposes. A user will have access to the Kyma Console only after you assign them to a proper role in the cockpit.



</td>
</tr>
<tr>
<td valign="top">

Namespace



</td>
<td valign="top">

Namespaces are used to organize objects in a cluster and provide a way to divide cluster resources. This way, several users can share a cluster but have access only to resources within the Namespace they have permissions for. This allows for increasing the security and organization of your cluster by dividing it into smaller units. Access to Namespaces in the Kyma environment depends on your permissions. SAP BTP users with the KymaRuntimeNamespaceAdmins role are entitled to create Namespaces, while users with the KymaRuntimeNamespaceDeveloper role can only list and edit Kubernetes and Kyma-specific resources scoped to specific Namespaces.



</td>
</tr>
<tr>
<td valign="top">

Service Catalog



</td>
<td valign="top">

A portfolio of SAP and non-SAP services available in the Kyma environment. These services expose their APIs or events in the Kyma environment and can extend your SAP solutions. To use them, you first have to create an instance of a given service in your Namespace and specify the consumption plan for it \(Service Plan\). Then, you must bind the instance with your SAP solution. Kyma environment also allows you to register cloud providers, such as Amazon Web Services \(AWS\), Microsoft Azure, or Google Cloud Platform \(GCP\) to extend the Service Catalog with additional services. See the official [Service Catalog documentation](https://svc-cat.io/docs/resources/#serviceinstance) for more details.



</td>
</tr>
<tr>
<td valign="top">

Service Plan



</td>
<td valign="top">

A representation of the costs and benefits for a given variant of a particular service in Service Catalog.



</td>
</tr>
<tr>
<td valign="top">

Binding



</td>
<td valign="top">

The connection you create between a service instance and an SAP solution so that they can communicate with each other. You can also bind a service instance to any workload running in the Kyma environment, such as a Function or a microservice.



</td>
</tr>
<tr>
<td valign="top">

Credentials / Secrets



</td>
<td valign="top">

Sensitive data necessary for an SAP solution to call the service, connect to it, and authenticate it. Depending on whether you use Kyma Console or kubectl to create the binding between a service instance and an SAP solution, the Kubernetes Secret object that contains these credentials is either created automatically or you need to create it manually.



</td>
</tr>
<tr>
<td valign="top">

Function



</td>
<td valign="top">

A simple code snippet that you can run without provisioning or managing servers. It implements the exact business logic you define. A Function is based on the Function custom resource and can be written in either Node.js or Python. A Function can perform a business logic of its own. You can also bind it to an instance of a service and configure it to be triggered whenever it receives a particular event type from the service or a call is made to the service's API. Functions are executed only if they are triggered by an event or an API call.



</td>
</tr>
<tr>
<td valign="top">

Microservice



</td>
<td valign="top">

An architectural variant for extensions or applications, where you separate the tasks into smaller pieces that interact with each other as loosely coupled, independently deployable units of code. A failing microservice should not cause your whole application to fail. Microservices are packed in a container that is always running; it's idling if there is no load. The microservice should always be reachable even when the Pods move around. Microservices typically communicate through APIs.



</td>
</tr>
</table>

