---
name: oci-security
description: "Implements threat detection, security posture enforcement, secrets management, WAF, and secure access for OCI workloads."
version: "1.0.0"
tags: ["oci", "security", "cloud-guard", "waf", "vault", "bastion"]
author: "Rahul Ganju"
---

# OCI Security Skill

## Overview
This skill implements **Cloud Guard, Security Zones, WAF, Vault/KMS, and Bastion** in Oracle Cloud Infrastructure. It enforces security posture, secrets management, threat detection, and secure access.  

> **Mandatory dependency:** Required for all production workloads.

---

## 5-Step Process

### Step 1: Discovery
- Identify data classification levels
- Inventory secrets
- Determine WAF needs
- Analyze Bastion access patterns
- Define encryption requirements
- Ensure compliance: PCI-DSS, HIPAA, SOC2

### Step 2: Analysis
- Cloud Guard detector/responder recipes
- Security Zone recipe restrictions
- Vault topology
- WAF rule sets
- Bastion session types
- Key lifecycle management

### Step 3: Creation

#### Cloud Guard (modules/security/cloud_guard.tf)
```hcl
resource "oci_cloud_guard_cloud_guard_configuration" "config" {
  compartment_id   = var.tenancy_ocid
  reporting_region = var.home_region
  status           = "ENABLED"
}

resource "oci_cloud_guard_target" "tenancy_target" {
  compartment_id       = var.tenancy_ocid
  display_name         = "tenancy-target"
  target_resource_id   = var.tenancy_ocid
  target_resource_type = "COMPARTMENT"
}
