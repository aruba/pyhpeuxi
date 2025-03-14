# pyhpeuxi

## HPE Aruba Networking User Experience Insight (UXI) SDK

This package has been developed in Python v3.9 to utilize the full functionality of the HPE Aruba Networking User Experience Insight API environment. Each available REST API command is available for use in this module. All responses from HPE Aruba Networking User Experience Insight API are in JSON format (converted into a Python dictionary object).

This package has been uploaded to [PyPI](https://pypi.org/) and is also available to install via [GitHub](https://github.com/aruba/pyhpeuxi). These instructions will also be available at [Aruba Developer Network](https://developer.arubanetworks.com/) in due course. Installation instructions and usage instructions are also provided below.

## Available API Categories

The following describes the available top-level API functionality of the HPE Aruba Networking User Experience Insight SDK available within this Python Package:
- API Service - Agents
- API Service - Agent Group Assignments
- API Service - Groups
- API Service - Network Group Assignments
- API Service - Sensors
- API Service - Sensor Group Assignments
- API Service - Service Tests Group Assignments
- API Service - Service Tests
- API Service - Wired Networks
- API Service - Wireless Networks

> [!WARNING]  
> This package comes without any warranties and should be used at your own risk.


## HPE Aruba Networking User Experience Insight (UXI) SDK API Prerequisites

As a prerequisite to using the onboarding API, the following conditions must be met:
1. Your dashboard must be on the HPE Greenlake Cloud Platform (GLP). If you are not yet migrated to the platform, you can follow these [steps to migrate via support](https://intercom.help/aruba-uxi/en/articles/10136432-migration-to-the-greenlake-cloud-platform).
2. Your dashboard must be using the new group-based configuration. We are beginning to migrate our customers to the new group-based configuration automatically beginning in February, but it may take a few months to complete for all dashboards. You can expedite the migration by following the [steps to prepare your dashboard for group-based configuration](https://intercom.help/aruba-uxi/en/articles/10355997-prepare-your-dashboard-for-group-based-configuration).

## HPE Aruba Networking User Experience Insight (UXI) SDK API Readiness

These steps list what is required on the HPE Aruba Networking User Experience Insight Management Console:
1. To get started with the UXI Onboarding API, first go to your Greenlake Cloud Workspace and select **Manage Workspace**.
2. Next, select the option for **Personal API clients** and select **Create Personal API Client**.
3. In the pop-up menu, provide a personal API client name and select the service for User Experience Insight (US West). Then select **Create Personal API client**.
4. You will then be given a Client ID and Client secret. Store these values locally in a safe location. These can be used within your script or you can use the API token provided in the next step. Note the access token described below is only valid for a short period of time.
5. When you look at the page for personal API clients again, you will see the one you created. Expand the menu to generate an access token using the client secret. This access token will be used for API requests.

If you need further information, refer to the HPE Aruba Networking User Experience Insight configuration documentation for the API account - [User Experience Insight Onboarding API](https://help.capenetworks.com/en/articles/10488192-user-experience-insight-onboarding-api).

# Python Requirements  
Ensure Python v3 or greater is installed on your operating system
# Package Installation

#### Method 1 - Installing Package from PyPi
Run the following in a command line terminal to install the pip package - ```pip3 install pyhpeuxi``` or ```pip install pyhpeuxi```. This may vary between Operating Systems. 

#### Method 2 - Installing Package from Github (not using Git.exe)
1. Click into the Aruba Github Repository where the latest version of pyhpeuxi is located 
2. Click Code (in green) and Download to Zip
3. Extract the zip file into a directory
4. Go into a command line terminal and change directory (cd) into the folder where you extracted the zipped file and then down one child folder. The folder contents should pyhpeuxi (FOLDER), LICENCE, pyproject.toml and README.md   
5. In your command line terminal type ```python3 -m build``` or ```python -m build```. This will create a folder called dist with a file containing a .gz extension. 
6. Run the following in a command line terminal to install the pip package - ```pip3 install pathtozip.gz``` or ```pip install pathtozip.gz```. This may vary between Operating Systems.

#### Method 3 - Installing Package from Github (using Git.exe)
1. Install Git for your Operating System from https://git-scm.com/download
2. Run the following in a command line terminal to install the pip package - ```pip3 install git+https://github.com/aruba/pyhpeuxi``` or ```pip install git+https://github.com/aruba/pyhpeuxi```. This may vary between Operating Systems. 

# Initial Usage Instructions

Within your favourite Python IDE environment, create an import reference. 

```python
from pyhpeuxi import *
```

Create a object to login into the API. The login object needs to be passed to use any function to use the API.  
Four examples below show how to create the login object (choose only one method).

1. Using API Token

```python
login = HPEUXIApiLogin(api_token="your API Token"))
```

2. Using API Client Credentials 
```python
login = HPEUXIApiLogin(client_id="your client id",client_secret="your client secret"))
```
3. Using the API Client Credentials retrieved from a JSON structured file. The file must exist in the same working directory of the script and contain the following structure. ```{"client_id":"your_client_id","client_secret":"your_client_secret"}```
```python
apiCreds = Utils_UXI.get_personal_api_client_creds_from_file("your_cred_file.token")
login = HPEUXIApiLogin(api_client_credentials=apiCreds)
```
4. Using API Token retrieved from a JSON structured file. The file must exist in the same working directory of the script and contain the following structure. ```{"access_token":"your_secret_token"}```
```python
apiToken = Utils_UXI.get_token_from_file("my_token_file.token")
login = HPEUXIApiLogin(api_token=apiToken)
```

> [!WARNING]  
> Never expose your credentials directly in your scripts. The above is just an example for completeness and to get you going. When using the likes of github, use your ignores file to exlude the credential files. 

> [!NOTE]  
> When using Method 2 to use the API of the UXI environment, you can retrieve the API token by calling the login variable and referencing the vaiable api_token ```(login.api_token)```. The API Tokens expire after 120 minutes. 

Find an API you want to use, by prefixing  `OpenApi.`  in your IDE and Intellisense will show the available APIs.  

The example below prints the contents of all the groups within the UXI environment. You must pass in the login variable to execute to function correctly.

```python
print(OpenApi.get_networks_wireless(login)) 
```
## Working Example
Below is an example of the initial usage instructions, which includes a console print to display the result.
```python
from pyhpeuxi import *
login = HPEUXIApiLogin(client_id="your client id",client_secret="your client secret")
print(OpenApi.get_networks_wireless(login)) 
```

## Optional Parameters
The following detail the additional available parameters within the HPEUXIApiLogin class. 
```python
verify_ssl = False, #Disable SSL if required. By default, verify SSL is enabled. 	
url = "https://api.capenetworks.com") # Override the API Service URL. Default URL is shown 
oauth_token_url = "https://sso.common.cloud.hpe.com/as/token.oauth2", #Override the GreenLake OAuth Token Service URL. The default URL is shown 
```

# Help

After writing a specific API call such as `OpenApi.function_name(`, you can hover your cursor over the command to view help information and the required parameters (e.g., in Visual Studio Code). Note that the first parameter is always "login." Additionally, you can read the function's help documentation by calling help(OpenApi.function_name). Each function includes a concise help summary.

## Full Function List
The following list details all the available functions within this package. Please use the help function described earlier to understand how to use each function. 

**Agent Functions (OpenApi Class)**
* delete_agent
* delete_group_agent
* get_agents
* get_group_agent
* new_group_agent
* update_agent

**Group Functions (OpenApi Class)**
* delete_group
* get_groups
* update_group
* new_group

**Network Group Functions (OpenApi Class)**
* delete_group_network
* get_group_network
* new_group_network

**Sensor Functions (OpenApi Class)**
* get_group_sensor
* get_sensors
* update_sensor
* new_group_sensor

**Service Functions (OpenApi Class)**
* delete_test_service
* get_test_service
* get_tests_service
* new_test_service

**Wireless / Wired Networks (OpenApi Class)**
* get_networks_wired
* get_networks_wireless

**Utilities (Utils_UXI Class)**
* get_personal_api_client_creds_from_file
* get_token_from_file
* export_to_csv

# Python Package Upgrade Instructions

Once an update is available on the Python PyPi repository, you may upgrade your release by completing the following in a command line terminal - 

`pip3 install pyhpeuxi --upgrade`  
or  
`pip install pyhpeuxi --upgrade`

To install a specific version, execute the following command with x.x.x being the specific version number you want to install. 

`pip3 install pyhpeuxi==x.x.x`  
or  
 `pip install pyhpeuxi==x.x.x`
 
# Uninstall Package Package

To remove the Python pyhpeuxi package, type the following command into a command line terminal -  
`pip3 uninstall pyhpeuxi `  
or  
 `pip uninstall pyhpeuxi `

# Further Usage Examples

These are just a few examples but there are many API functions available within the UXI SDK. 

## Move an Agent to another Group

This example requires the Client ID, Client Secret, the Agent Name and the Name of the Group to move the Agent To. 
``` Python
# import pyhpeuxi Module
from pyhpeuxi import *

# Login Credentials 
client_id="Your Client ID"
client_secret="Your Client Secret"

# Login Object
login_cred = HPEUXIApiLogin(client_id=client_id,client_secret=client_secret)

#### Parameters for Agent Name & New Group ####
agentName = "agentName"
moveAgentToGroup = "GroupName"
#### Parameters ####

# Get agents and return agentID if it matches the agentName variable
agents = OpenApi.get_agents(login_cred) 
agentID=""
for agent in agents['items']:
    if agent['name'] == agentName:
        agentID = agent['id']
        print("Agent details that have been matched:",agent)

# Get agents and return groupID if it matches the moveAgentToGroup variable
groups = OpenApi.get_groups(login_cred)
groupID = ""
for group in groups['items']:
    if group['name'] == moveAgentToGroup:
        print("Group Name Matched",moveAgentToGroup, " Group ID:",group['id'])
        groupID = group['id']

# Move agent to new group if obtained groupID and agentID 
if agentID and groupID:
    body={
    'groupId' : groupID, # The unique identifier of the group
    'agentId' : agentID, # The unique identifier of the agent
    }
    print(f'Moving Agent {agentName} to Group {moveAgentToGroup}, Output is: {OpenApi.new_group_agent(login_cred,body=body)}')
```

## Rename Agent

The following example renames an Agent and requires the Client ID, Client Secret, the old (current) Agent Name and the New Agent Name.

``` Python
from pyhpeuxi import *
#login credentials 
client_id="Your Client ID"
client_secret="Your Client Secret"

login_cred = HPEUXIApiLogin(client_id=client_id,client_secret=client_secret)
gg = OpenApi.get_groups(login_cred)
agents = OpenApi.get_agents(login_cred)

#Script Parameters #
oldAgentName = 'RXE40OHO5S'
newAgentName = 'RXE40OHO5S_Lab'
#Script Parameters #

print("Agent Details:",agents)

agentID=""
for agent in agents['items']:
    if oldAgentName == agent['name']:
        print("Found Agent",agent['name'])
        agentID = agent['id']

if agentID :
    body={'name' : newAgentName, 'notes' : 'Lab Agent - Windows 10 Work Machine'}
    print("Updating Agent Name and Notes:",OpenApi.update_agent(login_cred,id=agentID,body=body))
```
## Export Inventory to CSV

In the following example, we get a complete inventory of all our resources and write the data to a collection of CSV files in a folder called csv. This can be useful for inventory management, reporting and obtaining resource ID's for when we need to make additional calls to the onboarding API.

``` Python
import csv
import os
from pyhpeuxi import *

client_id="Your Client ID"
client_secret="Your Client Secret"

login_cred = HPEUXIApiLogin(client_id=client_id,client_secret=client_secret)

agents = OpenApi.get_agents(login_cred)
groups = OpenApi.get_groups(login_cred)
sensors = OpenApi.get_sensors(login_cred)
wiredNetworks = OpenApi.get_networks_wired(login_cred)
wirelessNetworks = OpenApi.get_networks_wireless(login_cred)
serviceTests = OpenApi.get_tests_service(login_cred)


Utils_UXI.export_to_csv(agents,'agents')
Utils_UXI.export_to_csv(groups,'groups')
Utils_UXI.export_to_csv(sensors,'sensors')
Utils_UXI.export_to_csv(wiredNetworks,'wiredNetworks')
Utils_UXI.export_to_csv(wirelessNetworks,'wirelessNetworks')
Utils_UXI.export_to_csv(serviceTests,'serviceTests')
```
