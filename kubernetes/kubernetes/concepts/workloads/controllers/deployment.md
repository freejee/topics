# [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)




+ [Use Case](#use-case)
+ [Creating a Deployment](#creating-a-deployment)
    + [Pod-template-hash label](#pod-template-hash-label)
+ [Updating a Deployment](#updating-a-deployment)
    + [Rollover (aka multiple updates in-flight)](#rollover-aka-multiple-updates-in-flight)
    + [Label selector updates](#label-selector-updates)
+ [Rolling Back a Deployment](#rolling-back-a-deployment)
    + [Checking Rollout History of a Deployment](#checking-rollout-history-of-a-deployment)
    + [Rolling Back to a Previous Revision](#rolling-back-to-a-previous-revision)
+ [Scaling a Deployment](#scaling-a-deployment)
    + [Proportional scaling](#proportional-scaling)
+ [Pausing and Resuming a Deployment](#pausing-and-resuming-a-deployment)
+ [Deployment status](#deployment-status)
    + [Progressing Deployment](#progressing-deployment)
    + [Complete Deployment](#complete-deployment)
    + [Failed Deployment](#failed-deployment)
    + [Operating on a failed deployment](#operating-on-a-failed-deployment)
+ [Clean up Policy](#clean-up-policy)
+ [Use Cases](#use-cases)
    + [Canary Deployment](#canary-deployment)
+ [Writing a Deployment Spec](#writing-a-deployment-spec)
    + [Pod Template](#pod-template)
    + [Replicas](#replicas)
    + [Selector](#selector)
    + [Strategy](#strategy)
        + [Recreate Deployment](#recreate-deployment)
        + [Rolling Update Deployment](#rolling-update-deployment)
            + [Max Unavailable](#max-unavailable)
            + [Max Surge](#max-surge)
    + [Progress Deadline Seconds](#progress-deadline-seconds)
    + [Min Ready Seconds](#min-ready-seconds)
    + [Rollback To](#rollback-to)
    + [Revision History Limit](#revision-history-limit)
    + [Paused](#paused)
+ [Alternative to Deployments](#alternative-to-deployments)
    + [kubectl rolling update](#kubectl-rolling-update)



## Use Case

## Creating a Deployment

### Pod-template-hash label

## Updating a Deployment

### Rollover (aka multiple updates in-flight)

### Label selector updates

## Rolling Back a Deployment

### Checking Rollout History of a Deployment

### Rolling Back to a Previous Revision

## Scaling a Deployment

### Proportional scaling

## Pausing and Resuming a Deployment

## Deployment status

### Progressing Deployment

### Complete Deployment

### Failed Deployment

### Operating on a failed deployment

## Clean up Policy

## Use Cases

### Canary Deployment

## Writing a Deployment Spec

### Pod Template

### Replicas

### Selector

### Strategy

#### Recreate Deployment

#### Rolling Update Deployment

##### Max Unavailable

##### Max Surge

### Progress Deadline Seconds

### Min Ready Seconds

### Rollback To

### Revision History Limit

### Paused

## Alternative to Deployments

### kubectl rolling update
































