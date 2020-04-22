# wabtec-maintenance-runbook
This repo is a maintenance checklist for wabtec to maintenance of MKE

## When to use
This repo should be used as che checklist for performing maintenance on DC/OS and MKE running inside DC/OS. A few examples would be as below 
1. Scaling the cluster resources 
2. Changing the cluster configurations
3. Fixing a broken cluster 


## Backups 
This is a higly debated/discusssed topic in Wabtec so I would  discuss them here to have some record and below is some glassary that would helo understand what is what 

1. "dcos kubernetes backup"  Offical DC/OS backup(Ark based) that backsup Kubernetes and also Kuberenetes cluster                configurations which means your cluster sizings and design etc. ARK is being upgraded by D2iQ and in future versions it      would run velero instead of Arc and hence should be the defacto method of backup and restore, check with you operator/D2iq    resource for latest updates. 
2. "velero backup" This is an open-source tool that later version of Ark. This backs up on Kubernetes but not backup the        kubernetes cluster configurations that "dcos kuberentes backup" does.  

### Procedure 
Note: These steps are for wabtec only 

1. Review the changes with changes with Operator and Architects 
2. Finalise on the maintenance window both durations and timeline 
3. Ensure all the k8s backs up taken are healthy and adhere to the RPO standards agreed by Wabtec&Application team
    a. This would mean valero backup currently but in future it would "dcos kubernetes backup" (see above for info)
    b. It was noted that backups do not include the extenal ELB-LB endpoints for Kong so restore would need changes from app          team as well due to this fact
4. Ensure all the DC/OS backups are taken including zookeeper as an added layer of protection 
5. Before performing the maintenance ensure all the compoenents of DC/OS and Kubernetes healthy, you could either run cli        commands or go the UI or Datadog dashboard to ensure everything is healthy. If problems are detected please work on fixing
   them before updates are set up
   NOTE: Performaing maintenance on a degraded cluster does not gaurantee results so its highly recommeneded to do                    maintenance on a healhty cluster 
6. Proceed with the maintenance. 
7. If succeeds then all is well. If it does not. Use the backups to restore and re-evaluate future steps with the Operator      and Architect 
