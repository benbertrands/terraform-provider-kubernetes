---
subcategory: "autoscaling/v2"
page_title: "Kubernetes: kubernetes_horizontal_pod_autoscaler_v2"
description: |-
  Horizontal Pod Autoscaler automatically scales the number of pods in a replication controller, deployment or replica set based on observed CPU utilization.
---

# kubernetes_horizontal_pod_autoscaler_v2

Horizontal Pod Autoscaler automatically scales the number of pods in a replication controller, deployment or replica set based on observed CPU utilization.

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `metadata` (Block List, Min: 1, Max: 1) Standard horizontal pod autoscaler's metadata. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata (see [below for nested schema](#nestedblock--metadata))
- `spec` (Block List, Min: 1, Max: 1) Behaviour of the autoscaler. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status (see [below for nested schema](#nestedblock--spec))

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--metadata"></a>
### Nested Schema for `metadata`

Optional:

- `annotations` (Map of String) An unstructured key value map stored with the horizontal pod autoscaler that may be used to store arbitrary metadata. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
- `generate_name` (String) Prefix, used by the server, to generate a unique name ONLY IF the `name` field has not been provided. This value will also be combined with a unique suffix. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#idempotency
- `labels` (Map of String) Map of string keys and values that can be used to organize and categorize (scope and select) the horizontal pod autoscaler. May match selectors of replication controllers and services. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
- `name` (String) Name of the horizontal pod autoscaler, must be unique. Cannot be updated. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names
- `namespace` (String) Namespace defines the space within which name of the horizontal pod autoscaler must be unique.

Read-Only:

- `generation` (Number) A sequence number representing a specific generation of the desired state.
- `resource_version` (String) An opaque value that represents the internal version of this horizontal pod autoscaler that can be used by clients to determine when horizontal pod autoscaler has changed. More info: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#concurrency-control-and-consistency
- `uid` (String) The unique in time and space value for this horizontal pod autoscaler. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#uids


<a id="nestedblock--spec"></a>
### Nested Schema for `spec`

Required:

- `max_replicas` (Number) Upper limit for the number of pods that can be set by the autoscaler.
- `scale_target_ref` (Block List, Min: 1, Max: 1) Reference to scaled resource. e.g. Replication Controller (see [below for nested schema](#nestedblock--spec--scale_target_ref))

Optional:

- `behavior` (Block List, Max: 1) Behavior configures the scaling behavior of the target in both Up and Down directions (`scale_up` and `scale_down` fields respectively). (see [below for nested schema](#nestedblock--spec--behavior))
- `metric` (Block List) The specifications for which to use to calculate the desired replica count (the maximum replica count across all metrics will be used). The desired replica count is calculated multiplying the ratio between the target value and the current value by the current number of pods. Ergo, metrics used must decrease as the pod count is increased, and vice-versa. See the individual metric source types for more information about how each type of metric must respond. If not set, the default metric will be set to 80% average CPU utilization. (see [below for nested schema](#nestedblock--spec--metric))
- `min_replicas` (Number) Lower limit for the number of pods that can be set by the autoscaler, defaults to `1`.
- `target_cpu_utilization_percentage` (Number) Target average CPU utilization (represented as a percentage of requested CPU) over all the pods. If not specified the default autoscaling policy will be used.

<a id="nestedblock--spec--scale_target_ref"></a>
### Nested Schema for `spec.scale_target_ref`

Required:

- `kind` (String) Kind of the referent. e.g. `ReplicationController`. More info: http://releases.k8s.io/HEAD/docs/devel/api-conventions.md#types-kinds
- `name` (String) Name of the referent. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names

Optional:

- `api_version` (String) API version of the referent


<a id="nestedblock--spec--behavior"></a>
### Nested Schema for `spec.behavior`

Optional:

- `scale_down` (Block List) Scaling policy for scaling Down (see [below for nested schema](#nestedblock--spec--behavior--scale_down))
- `scale_up` (Block List) Scaling policy for scaling Up (see [below for nested schema](#nestedblock--spec--behavior--scale_up))

<a id="nestedblock--spec--behavior--scale_down"></a>
### Nested Schema for `spec.behavior.scale_down`

Required:

- `policy` (Block List, Min: 1) List of potential scaling polices which can be used during scaling. At least one policy must be specified, otherwise the scaling rule will be discarded as invalid. (see [below for nested schema](#nestedblock--spec--behavior--scale_down--policy))

Optional:

- `select_policy` (String) Used to specify which policy should be used. If not set, the default value Max is used.
- `stabilization_window_seconds` (Number) Number of seconds for which past recommendations should be considered while scaling up or scaling down. This value must be greater than or equal to zero and less than or equal to 3600 (one hour). If not set, use the default values: - For scale up: 0 (i.e. no stabilization is done). - For scale down: 300 (i.e. the stabilization window is 300 seconds long).

<a id="nestedblock--spec--behavior--scale_down--policy"></a>
### Nested Schema for `spec.behavior.scale_down.policy`

Required:

- `period_seconds` (Number) Period specifies the window of time for which the policy should hold true. PeriodSeconds must be greater than zero and less than or equal to 1800 (30 min).
- `type` (String) Type is used to specify the scaling policy: Percent or Pods
- `value` (Number) Value contains the amount of change which is permitted by the policy. It must be greater than zero.



<a id="nestedblock--spec--behavior--scale_up"></a>
### Nested Schema for `spec.behavior.scale_up`

Required:

- `policy` (Block List, Min: 1) List of potential scaling polices which can be used during scaling. At least one policy must be specified, otherwise the scaling rule will be discarded as invalid. (see [below for nested schema](#nestedblock--spec--behavior--scale_up--policy))

Optional:

- `select_policy` (String) Used to specify which policy should be used. If not set, the default value Max is used.
- `stabilization_window_seconds` (Number) Number of seconds for which past recommendations should be considered while scaling up or scaling down. This value must be greater than or equal to zero and less than or equal to 3600 (one hour). If not set, use the default values: - For scale up: 0 (i.e. no stabilization is done). - For scale down: 300 (i.e. the stabilization window is 300 seconds long).

<a id="nestedblock--spec--behavior--scale_up--policy"></a>
### Nested Schema for `spec.behavior.scale_up.policy`

Required:

- `period_seconds` (Number) Period specifies the window of time for which the policy should hold true. PeriodSeconds must be greater than zero and less than or equal to 1800 (30 min).
- `type` (String) Type is used to specify the scaling policy: Percent or Pods
- `value` (Number) Value contains the amount of change which is permitted by the policy. It must be greater than zero.




<a id="nestedblock--spec--metric"></a>
### Nested Schema for `spec.metric`

Required:

- `type` (String) type is the type of metric source. It should be one of "ContainerResource", "External", "Object", "Pods" or "Resource", each mapping to a matching field in the object. Note: "ContainerResource" type is available on when the feature-gate HPAContainerMetrics is enabled

Optional:

- `container_resource` (Block List, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--container_resource))
- `external` (Block List, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--external))
- `object` (Block List, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--object))
- `pods` (Block List, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--pods))
- `resource` (Block List, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--resource))

<a id="nestedblock--spec--metric--container_resource"></a>
### Nested Schema for `spec.metric.container_resource`

Required:

- `container` (String) name of the container in the pods of the scaling target
- `name` (String) name of the resource in question

Optional:

- `target` (Block List, Max: 1) target specifies the target value for the given metric (see [below for nested schema](#nestedblock--spec--metric--container_resource--target))

<a id="nestedblock--spec--metric--container_resource--target"></a>
### Nested Schema for `spec.metric.container_resource.target`

Required:

- `type` (String) type represents whether the metric type is Utilization, Value, or AverageValue

Optional:

- `average_utilization` (Number) averageUtilization is the target value of the average of the resource metric across all relevant pods, represented as a percentage of the requested value of the resource for the pods. Currently only valid for Resource metric source type
- `average_value` (String) averageValue is the target value of the average of the metric across all relevant pods (as a quantity)
- `value` (String) value is the target value of the metric (as a quantity).



<a id="nestedblock--spec--metric--external"></a>
### Nested Schema for `spec.metric.external`

Required:

- `metric` (Block List, Min: 1, Max: 1) metric identifies the target metric by name and selector (see [below for nested schema](#nestedblock--spec--metric--external--metric))

Optional:

- `target` (Block List, Max: 1) target specifies the target value for the given metric (see [below for nested schema](#nestedblock--spec--metric--external--target))

<a id="nestedblock--spec--metric--external--metric"></a>
### Nested Schema for `spec.metric.external.metric`

Required:

- `name` (String) name is the name of the given metric

Optional:

- `selector` (Block List) selector is the string-encoded form of a standard kubernetes label selector for the given metric When set, it is passed as an additional parameter to the metrics server for more specific metrics scoping. When unset, just the metricName will be used to gather metrics. (see [below for nested schema](#nestedblock--spec--metric--external--metric--selector))

<a id="nestedblock--spec--metric--external--metric--selector"></a>
### Nested Schema for `spec.metric.external.metric.selector`

Optional:

- `match_expressions` (Block List) A list of label selector requirements. The requirements are ANDed. (see [below for nested schema](#nestedblock--spec--metric--external--metric--selector--match_expressions))
- `match_labels` (Map of String) A map of {key,value} pairs. A single {key,value} in the matchLabels map is equivalent to an element of `match_expressions`, whose key field is "key", the operator is "In", and the values array contains only "value". The requirements are ANDed.

<a id="nestedblock--spec--metric--external--metric--selector--match_expressions"></a>
### Nested Schema for `spec.metric.external.metric.selector.match_expressions`

Optional:

- `key` (String) The label key that the selector applies to.
- `operator` (String) A key's relationship to a set of values. Valid operators ard `In`, `NotIn`, `Exists` and `DoesNotExist`.
- `values` (Set of String) An array of string values. If the operator is `In` or `NotIn`, the values array must be non-empty. If the operator is `Exists` or `DoesNotExist`, the values array must be empty. This array is replaced during a strategic merge patch.




<a id="nestedblock--spec--metric--external--target"></a>
### Nested Schema for `spec.metric.external.target`

Required:

- `type` (String) type represents whether the metric type is Utilization, Value, or AverageValue

Optional:

- `average_utilization` (Number) averageUtilization is the target value of the average of the resource metric across all relevant pods, represented as a percentage of the requested value of the resource for the pods. Currently only valid for Resource metric source type
- `average_value` (String) averageValue is the target value of the average of the metric across all relevant pods (as a quantity)
- `value` (String) value is the target value of the metric (as a quantity).



<a id="nestedblock--spec--metric--object"></a>
### Nested Schema for `spec.metric.object`

Required:

- `described_object` (Block List, Min: 1, Max: 1) (see [below for nested schema](#nestedblock--spec--metric--object--described_object))
- `metric` (Block List, Min: 1, Max: 1) metric identifies the target metric by name and selector (see [below for nested schema](#nestedblock--spec--metric--object--metric))

Optional:

- `target` (Block List, Max: 1) target specifies the target value for the given metric (see [below for nested schema](#nestedblock--spec--metric--object--target))

<a id="nestedblock--spec--metric--object--described_object"></a>
### Nested Schema for `spec.metric.object.described_object`

Required:

- `api_version` (String) API version of the referent
- `kind` (String) Kind of the referent; More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds
- `name` (String) Name of the referent; More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names


<a id="nestedblock--spec--metric--object--metric"></a>
### Nested Schema for `spec.metric.object.metric`

Required:

- `name` (String) name is the name of the given metric

Optional:

- `selector` (Block List) selector is the string-encoded form of a standard kubernetes label selector for the given metric When set, it is passed as an additional parameter to the metrics server for more specific metrics scoping. When unset, just the metricName will be used to gather metrics. (see [below for nested schema](#nestedblock--spec--metric--object--metric--selector))

<a id="nestedblock--spec--metric--object--metric--selector"></a>
### Nested Schema for `spec.metric.object.metric.selector`

Optional:

- `match_expressions` (Block List) A list of label selector requirements. The requirements are ANDed. (see [below for nested schema](#nestedblock--spec--metric--object--metric--selector--match_expressions))
- `match_labels` (Map of String) A map of {key,value} pairs. A single {key,value} in the matchLabels map is equivalent to an element of `match_expressions`, whose key field is "key", the operator is "In", and the values array contains only "value". The requirements are ANDed.

<a id="nestedblock--spec--metric--object--metric--selector--match_expressions"></a>
### Nested Schema for `spec.metric.object.metric.selector.match_expressions`

Optional:

- `key` (String) The label key that the selector applies to.
- `operator` (String) A key's relationship to a set of values. Valid operators ard `In`, `NotIn`, `Exists` and `DoesNotExist`.
- `values` (Set of String) An array of string values. If the operator is `In` or `NotIn`, the values array must be non-empty. If the operator is `Exists` or `DoesNotExist`, the values array must be empty. This array is replaced during a strategic merge patch.




<a id="nestedblock--spec--metric--object--target"></a>
### Nested Schema for `spec.metric.object.target`

Required:

- `type` (String) type represents whether the metric type is Utilization, Value, or AverageValue

Optional:

- `average_utilization` (Number) averageUtilization is the target value of the average of the resource metric across all relevant pods, represented as a percentage of the requested value of the resource for the pods. Currently only valid for Resource metric source type
- `average_value` (String) averageValue is the target value of the average of the metric across all relevant pods (as a quantity)
- `value` (String) value is the target value of the metric (as a quantity).



<a id="nestedblock--spec--metric--pods"></a>
### Nested Schema for `spec.metric.pods`

Required:

- `metric` (Block List, Min: 1, Max: 1) metric identifies the target metric by name and selector (see [below for nested schema](#nestedblock--spec--metric--pods--metric))

Optional:

- `target` (Block List, Max: 1) target specifies the target value for the given metric (see [below for nested schema](#nestedblock--spec--metric--pods--target))

<a id="nestedblock--spec--metric--pods--metric"></a>
### Nested Schema for `spec.metric.pods.metric`

Required:

- `name` (String) name is the name of the given metric

Optional:

- `selector` (Block List) selector is the string-encoded form of a standard kubernetes label selector for the given metric When set, it is passed as an additional parameter to the metrics server for more specific metrics scoping. When unset, just the metricName will be used to gather metrics. (see [below for nested schema](#nestedblock--spec--metric--pods--metric--selector))

<a id="nestedblock--spec--metric--pods--metric--selector"></a>
### Nested Schema for `spec.metric.pods.metric.selector`

Optional:

- `match_expressions` (Block List) A list of label selector requirements. The requirements are ANDed. (see [below for nested schema](#nestedblock--spec--metric--pods--metric--selector--match_expressions))
- `match_labels` (Map of String) A map of {key,value} pairs. A single {key,value} in the matchLabels map is equivalent to an element of `match_expressions`, whose key field is "key", the operator is "In", and the values array contains only "value". The requirements are ANDed.

<a id="nestedblock--spec--metric--pods--metric--selector--match_expressions"></a>
### Nested Schema for `spec.metric.pods.metric.selector.match_expressions`

Optional:

- `key` (String) The label key that the selector applies to.
- `operator` (String) A key's relationship to a set of values. Valid operators ard `In`, `NotIn`, `Exists` and `DoesNotExist`.
- `values` (Set of String) An array of string values. If the operator is `In` or `NotIn`, the values array must be non-empty. If the operator is `Exists` or `DoesNotExist`, the values array must be empty. This array is replaced during a strategic merge patch.




<a id="nestedblock--spec--metric--pods--target"></a>
### Nested Schema for `spec.metric.pods.target`

Required:

- `type` (String) type represents whether the metric type is Utilization, Value, or AverageValue

Optional:

- `average_utilization` (Number) averageUtilization is the target value of the average of the resource metric across all relevant pods, represented as a percentage of the requested value of the resource for the pods. Currently only valid for Resource metric source type
- `average_value` (String) averageValue is the target value of the average of the metric across all relevant pods (as a quantity)
- `value` (String) value is the target value of the metric (as a quantity).



<a id="nestedblock--spec--metric--resource"></a>
### Nested Schema for `spec.metric.resource`

Required:

- `name` (String) name is the name of the resource in question.

Optional:

- `target` (Block List, Max: 1) Target specifies the target value for the given metric (see [below for nested schema](#nestedblock--spec--metric--resource--target))

<a id="nestedblock--spec--metric--resource--target"></a>
### Nested Schema for `spec.metric.resource.target`

Required:

- `type` (String) type represents whether the metric type is Utilization, Value, or AverageValue

Optional:

- `average_utilization` (Number) averageUtilization is the target value of the average of the resource metric across all relevant pods, represented as a percentage of the requested value of the resource for the pods. Currently only valid for Resource metric source type
- `average_value` (String) averageValue is the target value of the average of the metric across all relevant pods (as a quantity)
- `value` (String) value is the target value of the metric (as a quantity).







## Example Usage, with `metric`

```terraform
resource "kubernetes_horizontal_pod_autoscaler_v2" "example" {
  metadata {
    name = "test"
  }

  spec {
    min_replicas = 50
    max_replicas = 100

    scale_target_ref {
      kind = "Deployment"
      name = "MyApp"
    }

    metric {
      type = "External"
      external {
        metric {
          name = "latency"
          selector {
            match_labels = {
              lb_name = "test"
            }
          }
        }
        target {
          type  = "Value"
          value = "100"
        }
      }
    }
  }
}
```

## Example Usage, with `behavior`

```terraform
resource "kubernetes_horizontal_pod_autoscaler_v2" "example" {
  metadata {
    name = "test"
  }

  spec {
    min_replicas = 50
    max_replicas = 100

    scale_target_ref {
      kind = "Deployment"
      name = "MyApp"
    }

    behavior {
      scale_down {
        stabilization_window_seconds = 300
        select_policy                = "Min"
        policy {
          period_seconds = 120
          type           = "Pods"
          value          = 1
        }

        policy {
          period_seconds = 310
          type           = "Percent"
          value          = 100
        }
      }
      scale_up {
        stabilization_window_seconds = 600
        select_policy                = "Max"
        policy {
          period_seconds = 180
          type           = "Percent"
          value          = 100
        }
        policy {
          period_seconds = 600
          type           = "Pods"
          value          = 5
        }
      }
    }
  }
}
```

## Import

Horizontal Pod Autoscaler can be imported using the namespace and name, e.g.

```
$ terraform import kubernetes_horizontal_pod_autoscaler_v2.example default/terraform-example
```