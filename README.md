# AAP Execution Environment

## Pre-Req

1. Ansible core install on Linux vm
2. Ansible builder 
3. Python3
4. podman

## Steps:

Following steps reuqired to create custom EE environment. 

**1. Download EE base image from Automation Hub**

    a) login to linux server

    b) login to automation hub and download base image

      $ podman login <aap_hub_url> --tls-verify=false

      $ podman pull <aap_hub_url>/de-supported-rhel8 --tls-verify=false


**2. Update execution-environment.yml file - update URL to pull the base image from AAP HUB.**

Following section need to be update. 

    images:
      base_image:
        name: <aap_hub_url>/de-supported-rhel8:latest

**3. Update requirements.yml and requirements.txt file**

    requirements.yml file contain collections
    requirements.txt file contain python packages

**4. Run the Followig command to build the custom EE environment.**

       $ ansible-builder build -t <aap-hub-url>/<ee-name>:<tag>
       
       example:
       $ ansible-builder build -t aap-hub.telnetinfo.ca/ee-servicenow:v1

**5. Upload custom EE image to aap-hub**

       $ podman push <aap-hub-url>/<ee-name>:<tag> --tls-verify=false

       example:
       $ podman push aap-hub.telnetinfo.ca/ee-servicenow:v1 --tls-verify=false

