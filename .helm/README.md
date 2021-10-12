# Release spring-boot-dummy with Helm

## Release

````shell

export GITHUB_USERNAME=<GitHub username>>
export GITHUB_PAT=<GitHub PAT>
export OC_PROJECT=<OpenShift project/K8S namespace>
export RELEASE_NAME=mpbauer-playground-dummy-apps

helm install $RELEASE_NAME spring-boot-dummy \
--namespace $OC_PROJECT \
--set-string githubPatIssuer=$GITHUB_USERNAME \
--set-string githubPat=$GITHUB_PAT \
&& echo "---------------------------------------" \
&& helm get manifest $RELEASE_NAME | kubectl get -n $OC_PROJECT -f -
````

## Upgrade

````
helm upgrade $RELEASE_NAME spring-boot-dummy \
--namespace $OC_PROJECT \
--set-string global.githubPatIssuer=$GITHUB_USERNAME \
--set-string global.githubPat=$GITHUB_PAT \
&& echo "---------------------------------------" \
&& helm get manifest $RELEASE_NAME | kubectl get -n $OC_PROJECT -f -
````

## Delete 

````shell
export RELEASE_NAME=mpbauer-playground-dummy-apps 
export OC_PROJECT=dev

helm delete $RELEASE_NAME --namespace $OC_PROJECT
````