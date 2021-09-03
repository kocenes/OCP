# HTTP GET SAMPLES

```
SERVER=`oc whoami --show-server`  
TOKEN=`oc whoami --show-token`  
ENDPOINT=`oc whoami --show-server`  
NAMESPACE="XYZ"

```

### **Get list of deployment configs**
```
curl -ks -H "Authorization: Bearer $TOKEN" -H 'Accept: application/json' "$ENDPOINT/apis/apps.openshift.io/v1/deploymentconfigs" --insecure | jq '.items[] | "\(.metadata.namespace)/\(.metadata.name)"'
```

Output:
```scala
"telephone/communication-platform-v0"
"telephone-/script-management-business-v1"
"virtual/user-business-v0"
"virtual/web-channel-v0"
"workshop/example-app"
"workshop/lab-test-service-v0"
```

### **Get list of deployment configs in failed status**

```
curl -ks -H "Authorization: Bearer $TOKEN" -H 'Accept: application/json' "$ENDPOINT/apis/apps.openshift.io/v1/deploymentconfigs" --insecure | jq '.items[] | "\(.metadata.namespace)/\(.metadata.name)"'curl -ks -H "Authorization: Bearer $TOKEN" -H 'Accept: application/json' "$ENDPOINT/apis/apps.openshift.io/v1/deploymentconfigs" --insecure | jq '.items[] | select(.status.conditions[1].type == "Available" and .status.conditions[1].status == "False") | "\(.metadata.namespace)/\(.metadata.name)"'
```

Output:

```scala
"payment/statement-day-parameter-business-v2"
"payment/card-master-business-v0"
"people/customer-information-business-v1"
```

### **Get list of namespaces**

```
curl -ks -H "Authorization: Bearer $TOKEN" -H 'Accept: application/json' "$ENDPOINT/api/v1/namespaces" --insecure | jq -r ' .items[].metadata.name'
```
Output:
```scala
workflow-mgmt-engine-dev
workflow-mgmt-engine-qa
```