

VNF onboarding with Cloudify
============================

Zip structure:
/types - needed types for Standard TOSCA blueprints
/scripts - scripts used in configuration
OpenStack-inputs.yaml - inputs needed for Cloudify blueprint deployment, should be copied and filled outside the zip file 
mytest-OpenStack.yaml - Cloudify blueprint
mytest-OpenStack-TOSCA.yaml - Standard TOSCA blueprint
mytest-OpenStack-OSM.yaml - Standard TOSCA blueprint


Run your VNF with Cloudify and follow steps below.

1. Setup Cloudify virtualenv.
   
    You can skip this step if your virtualenv is already created and just activate it or use Cloudify UI instead.
    
    Using virtualenv:
    `virtualenv cloudify`
    `source cloudify/bin/activate`
    
    or using virtualenv wrapper:
    `mkvirtualenv cloudify`
    
    install cloudify cli:
    `pip install cloudify==3.4.1`
    
    Use cloudify manager:
    `cfy use -t <cfy manager ip>`

2. Install
    Fill inputs template with relevant data: OpenStack-inputs.yaml
    
    At once:
    `cfy install -l mytest-OpenStack.zip  -n mytest-OpenStack.yaml -b mytest --include-logs -i OpenStack-inputs.yaml`
    
    or step by step:
    `cfy blueprints publish-archive -l mytest-OpenStack.zip  -n mytest-OpenStack.yaml -b mytest-OpenStack`
    `cfy deployments create -d mytest-OpenStack -b mytest-OpenStack`
    `cfy executions -w install -d mytest-OpenStack --include-logs`

3. How to operate:

    Using UI or CLI. <information>
   
4. Uninstall 

    At once:
    `cfy uninstall -d mytest-OpenStack --include-logs`
    
    or step by step:
    `cfy executions -w uninstall -d mytest-OpenStack`
    `cfy deployments delete -d mytest-OpenStack`
    `cfy blueprints delete -b mytest-OpenStack`

