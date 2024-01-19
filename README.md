# AAP execution environment with validated collections

## Prerequisites

1. An offline token from [Red Hat Automation Hub](https://console.redhat.com/ansible/automation-hub) to pull the certified and validated collections (account required)
2. A RHEL system with 
   
## Building the execution environment image

1. Clone this repo and `cd` into the local repo directory.
```
git clone https://github.com/jce-redhat/ee-validated-example.git
cd ee-validated-example
```
2. Set the automation hub token environment variables, using the offline token generated on the Red Hat Automation Hub
```
export ANSIBLE_GALAXY_SERVER_CERTIFIED_TOKEN=<your_token>
export ANSIBLE_GALAXY_SERVER_VALIDATED_TOKEN=<your_token>
```
3. Run the ansible-builder command, passing in builder arguments that match the environment variables set above
```
ansible-builder build \
    --build-arg ANSIBLE_GALAXY_SERVER_CERTIFIED_TOKEN \
    --build-arg ANSIBLE_GALAXY_SERVER_VALIDATED_TOKEN \
    -v 3 \
    -t localhost/ee-validated-example:1.0
```
This will create an execution environment image called "localhost/ee-validated-example" with the tag set to "1.0".  An alternate version number can be used if desired.
4. Tag the new execution environment image with the "latest" tag
```
podman tag localhost/ee-validated-example:1.0 localhost/ee-validated-example:latest
```
