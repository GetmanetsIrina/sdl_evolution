
# Default CUSTOM_BUTTON subscription when HMI does not support

* Proposal: [SDL-NNNN](NNNN-Default_custom_button_subscription_when_HMI_does_not_support.md)
* Author: [Getmanets Irina](https://github.com/GetmanetsIrina)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

This proposal is about the handling the capabilities for CUSTOM_BUTTON.

## Motivation

Now SDL subscribes each application to CUSTOM_BUTTON by default by application registration and does not handle the capabilities for CUSTOM_BUTTON,
so in case HMI does not support CUSTOM_BUTTON SDL will subscribe application to CUSTOM_BUTTON anyway.

## Proposed solution

SDL can handle the capabilities for CUSTOM_BUTTON and in case HMI does not support CUSTOM_BUTTON,
SDL must NOT subscribe mobile application to CUSTOM_BUTTON during registration by default, it means SDL will not send Buttons.SubscribeButtons(CUSTOM_BUTTON) to HMI during application registration.


## Potential downsides

N/A

## Impact on existing code

* SDL core needs to be updated

## Alternatives considered

N/A
