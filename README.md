# PrivacyIDEA bMobi Token
<!-- TABLE OF CONTENTS -->
This is the documentation of Customized 3rd Party token integration for **bMobi** Mobile Application  

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
      <li>
      <a href="#configuration">Process of Token</a>
      <ul>
        <li><a href="#diagram-of-process">Diagram of Process</a></li>
        <li><a href="#process">Process</a>
        <ul>        
        <li><a href="#creation">1. Creation</a></li>
        <li><a href="#enrollment">2. Enrollment</a></li>
        <li><a href="#notification">3. Notification</a></li>
        <li><a href="#authentication">4. Authentication</a></li></ul>
        </li>
      </ul>
    </li>
    <li><a href="#contact">Contact</a></li>

  </ol>
</details>
<!-- Installation -->


### **Installation**

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
## **Configuration**
1. First click the **Config** button.

![PrivacyIdea Menu Screenshot][menu_config]

2. Then click the **Policies** button.

![PrivacyIdea Submenu Screenshot][menu_policy]

3. Then click **Create New Policy** button to add configuration for bmobi token.

![PrivacyIdea Create Policy Screenshot][create_policy]

4. Then fill the attributes as shown.
* **Policy Name**: any name can be used
* **Scope**: authentication
* **Priority**: 1

![PrivacyIdea Policy Name Screenshot][policy_name]

5. Fill the desired parameters that will be used to communicate with APIGATEWAY APIs that are in Action Section.
* APIGATEWAY authorized user's password (required)
* APIGATEWAY authorized username (required)
* APIGATEWAY rest API url (required) https://hermesdev.binghamton.edu/bmobi/privacyidea/triggerchallenge/
* timeout time of challenge (not required)


![PrivacyIdea bMobi Config Screenshot][bmobi_config]

<!-- Diagram -->
## **Diagram of Process**
Diagram of bMobi token process.
<img src="./images/token_process.svg">
<!-- Process -->

## **Process**
### Creation
1. User logins to binghamton account on mobile application which sends request with some details to APIGATEWAY.
2. APIGATEWAY creates bMobi token programatically, then gets the **enrollment_credentials** attributes that will be used in next steps.
```sh
GET /token/?serial=serial
```
* or
```sh
GET /token/?user=user&type=bmobi
```
### Enrollment
1. Without need an action from user, APIGATEWAY enrolls the token programatically.

**Required Parameters**

* The firebase token (that has been already sent by user while login process)
* Serial number of token
* Public Key
* Enrollment Credential

```sh
POST /ttype/bmobi?fbtoken=firebase_token&serial=token_serial_number&pubkey=public_key&enrollment_credentials=enrollment_credentials
```
2. If required parameters are correct, the body of the respose from API should contain;

* result: {
    status : true , 
    value : true 
    }
3. If value of result is **True**, this means token has been enrolled successfully.
 
### Notification
1. User triggers the two factor authentication challenge.

```sh
POST /validate/triggerchallenge?user=user&tpye=bmobi
```

2. PrivacyIDEA sends a request to APIGATEWAY
3. APIGATEWAY sends a push notification via Firebase Cloud Messaging to User's smartphone.
### Authentication
1. After getting push notification from APIGATEWAY, user decides Allow or Deny
2. If user press Allow, bMobi App sends a request to APIGATEWAY that contains signature and nonce
3. after recieving request from user, APIGATEWAY sends a confirmation to PrivacyIDEA

```sh
POST /ttype/bmobi?serial=serial&nonce=nonce&signature=signature
```

4. to Authenticate the user, PrivacyIDEA send a confirmation to CAS

<!-- CONTACT -->
## Contact

Efe Cankat Turkmen - cturkmen@binghamton.edu

Project Link: [https://github.com/BinghamtonUniversity/PrivacyIDEA_bMobi_Token#token-location](https://github.com/BinghamtonUniversity/PrivacyIDEA_bMobi_Token#token-location)

 
<!-- MARKDOWN LINKS & IMAGES -->
[menu_config]: images/menu_config.png
[all_config]: images/all_config.png
[create_policy]: images/create_policy.png
[menu_policy]: images/menu_policy.png
[policy_name]: images/policy_name.png
[bmobi_config]: images/bmobi_config.png
[pi_token_modules]: images/pi_token_modules.png
[bmobitoken.py]: bmobitoken.py
[token_process.svg]: images/token_process.svg

