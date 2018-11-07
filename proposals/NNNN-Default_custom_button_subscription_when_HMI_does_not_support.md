
# Avoid Custom button subscription in case HMI incompatibility 

* Proposal: [SDL-NNNN](NNNN-Default_custom_button_subscription_when_HMI_does_not_support.md)
* Author: [Getmanets Irina](https://github.com/GetmanetsIrina)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

In case if HMI does not support CUSTOM_BUTTON, SDL should not try to subscribe application to it.

## Motivation

Now SDL does not check hmi_capabilities before subscription to CUSTOM_BUTTON. So it will try to subscribe each registered application on `CUSTOM_BUTTON` even if it is unsupported by HMI.

SDL should check hmi capabilities and subscribe applicaiton to CUSTOM_BUTTON if it is **supported by HMI only**.

## Proposed solution

On application registration SDL should check hmi capabilities.

In case if CUSTOM_BUTTON is supported by hmi_capabilities : 
SDL should send `Buttons.SubscribeButtons(CUSTOM_BUTTON)` to HMI and wait for response. 


In case if CUSTOM_BUTTON is not supported by hmi_capabilities : 
SDL should **not** send `Buttons.SubscribeButtons(CUSTOM_BUTTON)` to HMI. 

If HMI support CUSTOM_BUTTON it should be in `Buttons[capabilites]` section of `hmi_capabilities.json` :

```
"Buttons": {
       "capabilities": [
        ..., 
        {
               "name": "CUSTOM_BUTTON",
               "shortPressAvailable": true,
               "longPressAvailable": true,
               "upDownAvailable": true
           }
        ]
}
```


If HMI support CUSTOM_BUTTON, response on `Buttons.GetCapabilities` should contain folowing structure :

```
"capabilities": [
        ..., 
        {
               "name": "CUSTOM_BUTTON",
               "shortPressAvailable": true,
               "longPressAvailable": true,
               "upDownAvailable": true
           }
        ]
```


`Buttons.GetCapabilities` request has higher proirity than `hmi_capabilities.json`.

## Potential downsides

N/A

## Impact on existing code

* SDL core needs to be updated

## Alternatives considered

N/A
