---
title: "How to Read & Write BMW MS43 EWS Alignment Data"
date: 2026-03-01
draft: false
difficulty: "beginner"
tags: ["ecu-programming", "bmw", "ms43", "ews"]
summary: "A beginner-friendly walkthrough on extracting and writing EWS (Electronic Immobilizer) alignment data from BMW MS43 DME units using INPA and NCS Expert."
---

## Prerequisites

- K+DCAN USB cable (FTDI chipset recommended)
- INPA 5.0+ or ISTA/D
- NCS Expert with latest DATEN files
- Laptop with Windows 7/10 (native COM port support)

## Step 1: Connect to the Vehicle

Plug your K+DCAN cable into the OBD-II port under the dashboard. Ensure INPA detects the DME module under **Engine > MS43**.

## Step 2: Read ISN from DME

Navigate to **Identification** in INPA. The ISN (Individual Serial Number) will be displayed as a 4-byte hex value. Write this down — you'll need it for alignment.

## Step 3: Read EWS Data

Switch to the EWS module. Read the current key data and note the stored ISN. If the ISN from the DME and EWS match, alignment is already correct.

## Step 4: Write New ISN

If installing a replacement DME, use NCS Expert to write the new DME's ISN into the EWS module. This requires Expert Mode access.

> ⚠️ **Warning**: Incorrect ISN alignment will prevent the vehicle from starting. Always back up both DME and EWS data before making changes.

## Verification

After writing, cycle the ignition off for 30 seconds, then attempt to start. The engine should crank and start within 2 seconds if alignment was successful.
