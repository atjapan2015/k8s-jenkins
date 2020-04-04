
```
helm install jenkins --set master.imagePullPolicy=IfNotPresent --set persistence.storageClass=local-path --namespace=public-service stable/jenkins
```
```
NAME: jenkins
LAST DEPLOYED: Sat Apr  4 19:02:10 2020
NAMESPACE: public-service
STATUS: deployed
REVISION: 1
NOTES:
1. Get your 'admin' user password by running:
  printf $(kubectl get secret --namespace public-service jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
2. Get the Jenkins URL to visit by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace public-service -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=jenkins" -o jsonpath="{.items[0].metadata.name}")
  echo http://127.0.0.1:8080
  kubectl --namespace public-service port-forward $POD_NAME 8080:8080

3. Login with the password from step 1 and the username: admin


For more information on running Jenkins on Kubernetes, visit:
https://cloud.google.com/solutions/jenkins-on-container-engine
```
```
  <securityRealm class="hudson.security.LDAPSecurityRealm" plugin="ldap@1.20">
    <disableMailAddressResolver>false</disableMailAddressResolver>
    <configurations>
      <jenkins.security.plugins.ldap.LDAPConfiguration>
        <server>ldap://ldap-service:389</server>
        <rootDN></rootDN>
        <inhibitInferRootDN>false</inhibitInferRootDN>
        <userSearchBase>dc=example,dc=org</userSearchBase>
        <userSearch>uid={0}</userSearch>
        <groupSearchBase>dc=example,dc=org</groupSearchBase>
        <groupMembershipStrategy class="jenkins.security.plugins.ldap.FromGroupSearchLDAPGroupMembershipStrategy">
          <filter></filter>
        </groupMembershipStrategy>
        <managerDN>cn=admin,dc=example,dc=org</managerDN>
        <managerPasswordSecret>ToDo</managerPasswordSecret>
        <displayNameAttributeName>uid</displayNameAttributeName>
        <mailAddressAttributeName>mail</mailAddressAttributeName>
        <ignoreIfUnavailable>false</ignoreIfUnavailable>
      </jenkins.security.plugins.ldap.LDAPConfiguration>
    </configurations>
    <userIdStrategy class="jenkins.model.IdStrategy$CaseInsensitive"/>
    <groupIdStrategy class="jenkins.model.IdStrategy$CaseInsensitive"/>
    <disableRolePrefixing>true</disableRolePrefixing>
  </securityRealm>
```
