### oc get clusteroperators
            operatorhub.io ---> operator registry
### oc get pods -n openshift-authentication-operator
### oc get pods -n openshift-authentication
### oc get pods -n openshift-file-integrity
### oc get packagemanifests -n openshift-marketplace
### oc get operatorgroup -n openshift-file-integrity
### oc get sub -n openshift-file-integrity
### oc describe packagemanifests file-integrity-operator -n openshift-marketplace |grep -i source
### oc get scv -n openshift-file-integrity  -->cluster service version
