# AAP EE

Following steps reuqired to create custom EE environment. 

servicenow and windows collections will be added into custom EE. Redhat and community collections already added into base image. 

**1. Update the ansible.cfg file**

    replace <AAP_HUB_URL> with approriate URL
    replace AAP_HUB_TOKEN with AAP HUB one time token.

    [galaxy]
        server_list = published_repo, rh-certified_repo
        ignore_certs = true
   
    [galaxy_server.published_repo]
        url = https://<AAP_HUB_URL>/api/galaxy/content/published/
        token=<AAP_HUB_TOKEN>
    
    [galaxy_server.rh-certified_repo]
        url=https://<AAP_HUB_URL>/api/galaxy/content/rh-certified/
        token=<AAP_HUB_TOKEN>
    
    [galaxy_server.community_repo]
        url=https://<AAP_HUB_URL>/api/galaxy/content/community/
        token=<AAP_HUB_TOKEN>

**2. Update execution-environment.yml file - update URL to pull the base image from AAP HUB.**

Following section need to be update. 

    images:
      base_image:
        name: <aap_hub_url>/ee-supported-rhel8:latest

**3. Run the Followig command to build the custom EE environment.**

       $ ansible-builder build -t <aap-hub-url>/<ee-name>:<tag>

**4. Upload custom EE image to aap-hub**

       $ podman push <aap-hub-url>/<ee-name>:<tag>

