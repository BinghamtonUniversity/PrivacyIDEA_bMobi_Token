# PrivacyIDEA bMobiToken
<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#installation">Installation</a>
      <ul>
        <li><a href="#pi-config-location">Pi config Location</a></li>
        <li><a href="#token-location">Token Location</a></li>
      </ul>
    </li>
    <li>
      <a href="#configuration">Configuration</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>

  </ol>
</details>
<!-- Installation -->


### Installation

### Pi config Location
To be able to list customized third party token, one line is needed to be added to pi.cfg file which is located as default below
* pi.cfg
  ```sh
  /etc/privacyidea/pi.cfg
  ```
#### Pi config Configuration

Following line is need to be added into pi.cfg file, so bmobitoken would show up into token list.
* PI_TOKEN_MODULES
  ```sh
  PI_TOKEN_MODULES = ["privacyidea.lib.tokens.bmobitoken"]
  ```
The example below shows how you can implement the line into pi.cfg file.
    ![PrivacyIdea pi.cfg Screenshot][pi_token_modules]
    
### Token Location
To install token one thing need to be done is; copy [bmobitoken.py] and then paste to location below.
* Default token location
  ```sh
  /opt/privacyidea/lib/python3.8/site-packages/privacyidea/lib/tokens/bmobitoken.py
  ```

<!-- Configuration -->
## Configuration
1. First click the **Config** button.

![PrivacyIdea Menu Screenshot][menu_config]

2. Then click the **Policies** button.

![PrivacyIdea Submenu Screenshot][menu_policy]

3. Then click **Create New Policy** button to add configuration for bmobi token.

![PrivacyIdea Create Policy Screenshot][create_policy]

4. Then fill the attributes as shown.
* **Policy Name**: any name can be used
* **Scope**: enrollment
* **Priority**: 1

![PrivacyIdea Policy Name Screenshot][policy_name]

5. Fill the desired parameters that will be used to communicate with APIGATEWAY APIs
* APIGATEWAY authorized user's password (required)
* APIGATEWAY authorized username (required)
* APIGATEWAY rest API url (required)
* timeout time of challenge (not required)


![PrivacyIdea bMobi Config Screenshot][bmobi_config]

 
<!-- MARKDOWN LINKS & IMAGES -->
[menu_config]: images/menu_config.png
[all_config]: images/all_config.png
[create_policy]: images/create_policy.png
[menu_policy]: images/menu_policy.png
[policy_name]: images/policy_name.png
[bmobi_config]: images/bmobi_config.png
[pi_token_modules]: images/pi_token_modules.png
[bmobitoken.py]: bmobitoken.py
