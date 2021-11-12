# PrivacyIDEA bMobiToken
<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#installation">Installation</a>
      <ul>
        <li><a href="#pi.cfg-location">Pi.cfg Location</a></li>
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

### Pi.cfg Location
To be able to list customized third party token, one line is needed to be added to pi.cfg file which is located as default below
* pi.cfg
  ```sh
  /etc/privacyidea/pi.cfg
  ```
#### pi.cfg Configuration
[pi_token_modules]
    
* PI_TOKEN_MODULES
  ```sh
  PI_TOKEN_MODULES = ["privacyidea.lib.tokens.bmobitoken"]
  ```
    ![PrivacyIdea pi.cfg Screenshot][pi_token_modules]
    
### Token Location
To install token one thing need to be done is; copy bmobitoken.py and then paste to location below.
* bmobitoken.py
  ```sh
  /opt/privacyidea/lib/python3.8/site-packages/privacyidea/lib/tokens/bmobitoken.py


<!-- Configuration -->
## Configuration

![PrivacyIdea Menu Screenshot][menu_config]
![PrivacyIdea Submenu Screenshot][menu_policy]
This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.



  ```
<!-- MARKDOWN LINKS & IMAGES -->
[menu_config]: images/menu_config.png
[all_config]: images/all_config.png
[create_policy]: images/create_policy.png
[menu_policy]: images/menu_policy.png
[policy_name]: images/policy_name.png
[bmobi_config]: images/bmobi_config.png
[pi_token_modules]: images/pi_token_modules.png