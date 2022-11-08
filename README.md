[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ebob9/meraki_prisma_access/blob/main/Meraki_%2B_Prisma_Access_Integration.ipynb)

# Meraki + Prisma Access Integration Script/GUI

#### Synopsis
This is an extremely simple and easy Meraki and Prisma Access integration GUI built using Google Colaboratory

#### Requirements
* Active Meraki Network and Subscription
* Active Prisma Access Subscription
* Python modules (installed automatically by Google Colaboratory):
    * Meraki Dashboard API SDK - <https://github.com/meraki/meraki-python-sdk> 
    * Prisma SASE SDK: prisma_sase - <https://github.com/PaloAltoNetworks/prisma-sase-sdk-python>

#### NOTES and LIMITATIONS:
* Meraki sites must be in a _"Third Party VPN"_ capable mode and contain devices that can perform these VPNs (MX, etc.)
* Due to limitations in the Meraki Third Party VPN public API, **ONLY Third Party Tunnels created by this integration may be present. All other Third Party Tunnels WILL BE DELETED.**
  * This integration limitation due specifically to the following Meraki API limitations:
    1. The Meraki "Third Party VPN" requires ALL TUNNELS network-wide to be re-sent when adding/removing/changing any single tunnel.
    2. The Meraki "Third Party VPN" API (correctly) does not return PSK details for configured tunnels.
* Any manual Meraki tunnels to Prisma Access will not show in the UI.
* Prisma Access subscription must be in "Aggregate Bandwidth" mode.
* Prisma Access administrator must allocate bandwidth to Remote Network region(s), or no region(s) will be present in this integration UI.
* The Integration defaults to the Prisma Access Cisco ISR Crypto profile. If another Crypto profile is configured in Prisma Access for these units, it will need to be switched.
* This Integration 

#### Using the Integration
1. [Launch the integration in Google Colaboratory.](https://colab.research.google.com/github/ebob9/meraki_prisma_access/blob/main/Meraki_%2B_Prisma_Access_Integration.ipynb)
2. Once launched, fill out the following fields:
  * `meraki_api_key`: Meraki Dashboard API Key
  * `pa_service_account`: Palo Alto Networks Tenant Service Group Account ID
  * `pa_secret`: Palo Alto Networks Tenant Service Group Account Secret
  * `pa_tsg_id`: Palo Alto Networks Tenant Service Group Unique Identifier
  * `PSK`: Pre-Shared key to be used by the tunnels
  * `EMAIL_TEMPLATE`: an email-format address (user@host.com) to be used as a template for the system to set up IKE authentication for the tunnels.
3. Once the above is filled out, hit "Play" on the **Meraki Integration Basic Information**
4. After a few seconds, the system should return `Done!` if successful with the inital setup.
5. Hit "Play" on the **Meraki Integration** section.
6. If setup is complete, you should see a table view of all Meraki Networks:

   [![Integration Notebook Screenshot](https://github.com/ebob9/meraki_prisma_access/raw/main/images/integration-example.png)]
7. To use the interface, simply select a region and SPN (Security Processing Node) for a site. 
8. Hit `Commit` to send changes to Meraki and Prisma Access.

Other buttons / options in the UI perform the following advanced functions:
* `Revert Pending Changes`: Resets the UI back to the original state (undoes changes)
* `Hard Refresh All`: Performs a full reload of the entire UI, reloading state from both Meraki and Prisma Access APIs.
* `Force VPN-IP Update`: Due to Prisma Access, some Meraki tunnels may not yet have their final IP after the commit finishes. These tunnels will have a placeholder peer of `127.0.0.1`. This button refreshes all Meraki Peer IP, and can be used to fill in any missing addresses.
* `Refresh Status`: This button refreshes the "Prisma Status", "Meraki Status", and "Tunnel Status" columns only.
* `Force Commit` checkboxes: These allow re/force committing a site. Normally, only networks with changes are committed. Networks with this check box will always be commited.

#### License
MIT

#### Version
| Version   | Changes                        |
|-----------|--------------------------------|
| **0.9.0** | Initial Github Public Release. |
