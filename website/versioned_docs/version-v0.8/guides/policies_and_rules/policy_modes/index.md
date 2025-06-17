---
slug: /guides/policies_and_rules/policy_modes
sidebar_position: 1
---

# The Policy Modes

## Overview
The modes can be specified through the `spec.policy.mode` field of [VarmorPolicy](../../getting_started/usage_instructions#varmorpolicy) or [VarmorClusterPolicy](../../getting_started/usage_instructions#varmorclusterpolicy) objects. The modes supported by different enforcers are shown in the following table.

|Policy Mode|AppArmor|BPF|Seccomp|Description|
|-----------|--------|---|-------|-----------|
|AlwaysAllow|✔️|✔️|✔️|No mandatory access control rules are imposed on container.|
|RuntimeDefault|✔️|✔️|✔️|Basic protection is provided by using the default profile of containerd. See [cri-containerd.apparmor.d](https://github.com/containerd/containerd/blob/main/contrib/apparmor/template.go) and [seccomp_default](https://github.com/containerd/containerd/blob/main/contrib/seccomp/seccomp_default.go).|
|EnhanceProtect|✔️|✔️|✔️|- Predefined [Built-in Rules](../built_in_rules/index.md) are ready to use out of the box.<br />- Tailor protection policies to specific requirements via customizable interfaces.<br />- Support Alarm-Only and Alarm-Interception modes for monitoring and auditing.<br />- Generate AppArmor/BPF profiles based on RuntimeDefault or AlwaysAllow modes.|
|BehaviorModeling|✔️|🏗️|✔️|- Uses BPF and audit technologies to perform behavior modeling across workloads.<br />- Behavior models are stored in the corresponding [ArmorProfileModel](https://github.com/bytedance/vArmor/blob/main/apis/varmor/v1beta1/armorprofilemodel_types.go) object.<br />- Does not support dynamic mode switching.<br />- See [BehaviorModeling Mode](behavior_modeling.md) for details.|
|DefenseInDepth|✔️|🏗️|✔️|- Provide Deny-by-Default protection via the behavior model or custom profiles.<br />- Provide custom rule interfaces and alarm-only mode to develop and manage profiles.<br />- See [DefenseInDepth Mode](defense_in_depth.md) for details.|

<br />

Note:
* vArmor policy supports dynamic switching of running modes (limited to AlwaysAllow, EnhanceProtect, RuntimeDefault, DefenseInDepth) and updating sandbox rules without having to restart the workloads. However, when using the **Seccomp enforcer**, the workload must be restarted for changes to the **Seccomp Profile** to take effect.
* vArmor supports modifying policies to add new enforcers, and the newly added enforcers only take effect on newly created Workloads.
* vArmor supports modifying policies to remove the BPF enforcer.

## Experimentals
import DocCardList from '@theme/DocCardList';

<DocCardList />
