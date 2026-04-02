---
title: "Blog 6"
date: 2026-04-01
weight: 6
chapter: false
pre: " <b> 3.6. </b> "
---

# AWS: Integrating Agents, Resilience, Security, Storage, and Game Protection

AWS continues to evolve across multiple fronts—model customization for enterprise AI, resilient identity and access patterns, operational tooling, deterministic security for agent-driven workflows, and specialized protections for latency-sensitive workloads like multiplayer games. This consolidated post synthesizes recent AWS announcements and guidance to highlight how organizations can safely adopt agentic capabilities while maintaining operational resilience and security.

---

## Custom Frontier Models and Responsible Specialization

AWS introduced new options for organizations that need models deeply aligned with private data and domain knowledge. Rather than relying only on prompt engineering or late-stage fine-tuning, services such as Amazon Nova Forge let customers start from early model checkpoints and blend proprietary data with curated training sets. This data-mixing approach reduces catastrophic forgetting and preserves foundational capabilities while enabling stronger domain specialization.

Key operational patterns:
- Start from an appropriate checkpoint (pre-, mid-, or post-training) to balance cost and control.
- Combine proprietary datasets with curated public or vendor datasets to retain general skills.
- Use managed training pipelines (for example via SageMaker AI) and integrated deployment targets (such as Bedrock) to shorten the path from model adaptation to production.

Responsible AI controls are critical during this process: safety tooling, moderation, and governance controls should be integrated into training and deployment workflows so that specialized models retain both capability and guardrails.

---

## Resilient Identity: Multi-Region Access and MCP-aware Authorization

As organizations deploy distributed applications and agent-driven automation, identity availability and locality matter. Multi-Region replication for IAM Identity Center allows workforce access and supported managed applications to operate even when a primary Region is disrupted. Replication requires coordination across KMS, IdP configuration, and networking, but yields improved availability and the ability to place applications nearer to users.

For AI-driven actions (for example via AWS-managed MCP servers), AWS has proposed IAM context keys to distinguish requests that originate via MCP services. These keys enable policy authors to:
- Block or restrict sensitive operations when a request comes through an MCP server.
- Allow read-only or limited operations while denying destructive actions like deletions.
- Map specific services to specific MCP servers (e.g., require EKS actions to flow through an EKS-specific MCP gateway).

Combining multi-Region identity and MCP-aware policies supports both resilience and tighter governance when agents perform privileged work across accounts and Regions.

---

## Operational Agents and Platform Evolution

Agentic tooling for cloud operations is maturing. AWS’s agent initiatives—ranging from DevOps-oriented agents to managed MCP servers that can call thousands of AWS APIs—make it possible for agents to orchestrate multi-step infrastructure tasks. To adopt these patterns safely, teams should:
- Reuse existing IAM models (least privilege) and apply context keys or service-specific controls for agent-originated requests.
- Stage agent rollout with log-only modes (observe before enforcing) and use CloudTrail to analyze agent behavior.
- Use region-local endpoints or multi-Region replication to keep latency and availability predictable for automation flows.

These practices reduce surprises when agents act at scale and make audits and incident response more tractable.

---

## Deterministic Policy Enforcement for Agent Safety

Securing agents requires moving critical authorization decisions outside of model reasoning. AWS AgentCore’s runtime policy model (built on Cedar-style semantics) is an example of deterministic, gateway-level enforcement that evaluates principal, action, and resource with explicit conditions.

Design guidance:
- Prefer default-deny policies and layered forbids to stop risky operations even when permissive rules exist.
- Author testable policies and run them in LOG_ONLY until validated.
- Use identity-scoped checks and request-parameter comparisons to ensure agents cannot elevate access or exfiltrate data by changing inputs.

This separation—agent reasoning vs. gateway enforcement—yields auditable, reproducible controls suitable for regulated environments like healthcare and finance.

---

## Specialized Protections: Multiplayer Gaming and DDoS

For latency-sensitive, UDP-based workloads such as multiplayer games, AWS introduced relay-based protections that authenticate clients, obfuscate server endpoints, and enforce per-player traffic limits. These designs emphasize proactive mitigation and low-latency operation rather than slow reactive rules.

Best practices for protective deployments:
- Integrate relay-based protections and tokenized access so game servers are not directly exposed.
- Test performance impact under real workloads; aim for negligible added latency.
- Combine network-level defenses with application-level visibility and CloudWatch monitoring to maintain operational awareness.

---

## Practical Next Steps for Teams

1. Inventory agent use cases and classify risk levels (read-only, administrative, destructive).
2. Apply least-privilege IAM, using MCP context keys to restrict agent-originated actions where needed.
3. Start agent deployments in `LOG_ONLY` or staged modes and analyze CloudTrail logs for unexpected behavior.
4. Where availability matters, adopt multi-Region Identity Center replication and region-local agent endpoints.
5. For regulated environments, combine VPC endpoint patterns with IAM controls to keep agent traffic private and auditable.

---

## Conclusion

The recent AWS advances demonstrate a consistent theme: make agent-driven automation more powerful, but pair it with controls that preserve resilience, auditability, and security. By blending adapted model training, multi-Region identity architectures, deterministic policy enforcement, and workload-specific protections, organizations can unlock agent productivity while managing risk.

## About the Authors

This post synthesizes insights from multiple AWS blog posts and product launches on model customization, identity and access, agent governance, storage and operational tooling, and game-protection features.
---
title: "Blog 6"
date: 2026-03-02
weight: 6
chapter: false
pre: " <b> 3.6. </b> "
---

# Understanding IAM for Managed AWS MCP Servers

As AI agents become more deeply integrated into software development workflows, organizations increasingly need a way to let those agents interact with AWS resources securely and consistently. In practice, this means AI agents should be able to use the same **AWS Identity and Access Management (IAM)** permissions model that developers already rely on, rather than forcing teams to create and manage a separate authorization system just for AI-driven activity. At the same time, organizations also need enough control to distinguish between actions performed directly by a human user and those initiated by an AI agent on that user’s behalf.

In this AWS Security Blog post, the authors explain how AWS is addressing that need for **AWS-managed remote Model Context Protocol (MCP) servers**. The post introduces new standardized IAM context keys that help organizations apply different governance policies to MCP-based AI activity, describes a simplified authorization model that aligns more closely with the behavior of the **AWS CLI** and **AWS SDKs**, and previews future support for **VPC endpoints** to add private network and perimeter-based controls.

---

## Overview

AWS explains that at **AWS re:Invent 2025**, the company launched four AWS-managed remote MCP servers in preview: **AWS**, **EKS**, **ECS**, and **SageMaker**. These AWS-managed MCP servers are hosted and maintained by AWS, which means customers do not need to install or manage local MCP server infrastructure themselves. Instead, they benefit from automatic updates, better scalability and resiliency, and auditability through **AWS CloudTrail**.

A key example highlighted in the post is the **AWS MCP Server**, which can provide access to AWS documentation and can execute calls to more than **15,000 AWS APIs**. This allows AI agents to assist with multi-step infrastructure and operations tasks such as provisioning VPC resources or configuring **Amazon CloudWatch** alarms.

However, AWS notes that customers raised two important concerns as AI agents began to play a larger role in development workflows. First, they wanted AI agents to work with their **existing IAM permissions**, rather than requiring a separate permission framework. Second, they wanted the flexibility to apply **different governance controls** to AI-driven actions than to human-initiated actions.

To address these needs, AWS introduced two new standardized IAM context keys for AWS-managed MCP servers:

- **`aws:ViaAWSMCPService`**
- **`aws:CalledViaAWSMCP`**

These context keys make it possible to identify whether a request came through an AWS-managed MCP server and, if so, which specific MCP server initiated the action. According to the post, this helps organizations implement **defense-in-depth**, maintain detailed audit trails, and satisfy compliance requirements by distinguishing AI-driven access from direct user actions.

In addition, AWS announced an upcoming simplification to the authorization model. Customers will soon no longer need to use separate **MCP-specific IAM actions** such as `aws-mcp:InvokeMCP` when interacting with AWS-managed MCP servers over public endpoints. Instead, the system will align more closely with how the AWS CLI and SDKs already work, reducing configuration complexity while continuing to rely on existing IAM policies for service access control.

Finally, AWS shared that **VPC endpoint support** for AWS-managed MCP servers is planned for the future. This will help organizations apply both **identity-based** and **network-based** controls, especially in highly regulated environments.

---

## Using IAM to differentiate between human-driven and AI-driven actions

A major theme of the post is the need for organizations to precisely control how AI agents access AWS resources. AWS introduces two standardized IAM context keys for this purpose.

### `aws:ViaAWSMCPService`

This is a **boolean** context key. It is set to `true` when a request comes through an AWS-managed MCP server. Administrators can use this key to broadly allow or deny actions initiated through any AWS-managed MCP server.

### `aws:CalledViaAWSMCP`

This is a **single-valued string** context key. It identifies the service principal of the MCP server that made the call, such as:

- `aws-mcp.amazonaws.com`
- `eks-mcp.amazonaws.com`
- `ecs-mcp.amazonaws.com`

This allows administrators to define policies that permit or deny access based on the **specific MCP server** involved. AWS also notes that as additional AWS-managed MCP servers become available, this key will support those new values as well, enabling more granular policy design over time.

These context keys can be used in both IAM policies and **service control policies (SCPs)** to implement fine-grained guardrails.

---

## Example: Denying all actions through MCP servers

The post gives an example of an organization that wants to completely disable AWS-managed MCP server access across an AWS Organization or within a specific organizational unit. This can be done by creating an SCP that denies all actions whenever the request is identified as coming through an MCP server.

The logic is straightforward: if `aws:ViaAWSMCPService` is `true`, then the request is denied.

This kind of policy is useful for organizations that want a conservative starting point for AI governance or need to prohibit AI-mediated infrastructure actions until internal review and approval processes are complete.

---

## Example: Allowing read-only Amazon S3 access but blocking deletes through MCP

Another example in the blog shows how an organization can allow AI agents to perform certain safe operations while blocking more sensitive ones.

In this case, the **AWS MCP Server** is allowed to perform read operations on **Amazon S3**, such as:

- `s3:GetObject`
- `s3:ListBucket`

At the same time, delete operations such as:

- `s3:DeleteObject`
- `s3:DeleteBucket`

are explicitly denied whenever the request comes through an MCP server, again using the `aws:ViaAWSMCPService` condition.

This demonstrates how organizations can let AI agents support productivity for low-risk activities while retaining stronger control over destructive or high-impact actions.

---

## Example: Restricting access to specific MCP servers

The post also describes how administrators can restrict access to certain AWS services so that they are only available through a specific MCP server.

For example, an organization might decide that **Amazon EKS** operations should only be permitted when initiated through the **EKS MCP server**, not through the broader AWS MCP server. In that case, the IAM policy can allow `eks:*` actions only when `aws:CalledViaAWSMCP` equals `eks-mcp.amazonaws.com`, and deny them otherwise.

This approach is valuable when different MCP servers are intended for different operational scopes. It allows organizations to map permissions more tightly to purpose-built AI interfaces rather than granting broad access through a single generalized server.

---

## Understanding the changes for public endpoint authorization

AWS says it heard from customers that the original authorization model for AWS-managed MCP servers added unnecessary complexity. In response, the company is simplifying the model so it behaves more like the AWS CLI and SDKs.

Under the upcoming approach, the MCP server still authenticates requests using **AWS Signature Version 4 (SigV4)**. However, instead of requiring separate MCP-specific IAM actions, the MCP server forwards the request to the downstream AWS service together with the standardized IAM context keys:

- `aws:ViaAWSMCPService`
- `aws:CalledViaAWSMCP`

The downstream AWS service then evaluates the request using the customer’s **existing IAM policies**, which can reference those context keys as needed.

This means organizations can continue using the same AWS credentials and service-level permissions they already manage today. AI agents can operate within those existing boundaries, while administrators gain a simpler and more familiar authorization model. AWS highlights that this eliminates the need for separate MCP-specific permissions for public endpoint authorization and reduces configuration overhead.

The blog includes a diagram showing this simplified authorization flow, in which the MCP server acts as the intermediary that authenticates the request, adds relevant context, and forwards it to the target AWS service for policy evaluation.

---

## Using IAM with MCP servers and VPC endpoints

The authors also discuss feedback from customers in regulated industries such as **financial services** and **healthcare**, where private network communication is often a compliance requirement. For these customers, identity-based controls alone may not be sufficient. They may also need to ensure that AI agent traffic does not traverse the public internet.

To address this, AWS plans to add **VPC endpoint support** for AWS-managed MCP servers. With this capability, customers will be able to connect to MCP servers directly from within their VPCs, keeping AI agent traffic inside their private network boundaries.

According to the post, this will create a **two-stage authorization model**:

1. An authorization check at the **VPC endpoint level**
2. A second authorization check at the **downstream AWS service level** using IAM policies

This layered approach strengthens security by combining **network perimeter controls** with **service-level identity controls**. AWS explains that customers will be able to combine VPC endpoints with the new IAM context keys to build more comprehensive governance models tailored to their security and compliance needs.

Additional implementation details and example patterns will be made available when VPC endpoint support is officially launched.

---

## Things to consider

The post concludes the technical discussion with several practical recommendations for customers adopting IAM-based authorization for MCP servers.

### Designing IAM policies carefully

AWS advises customers to grant only the permissions that are actually needed. As AI agents become more capable and usage patterns become clearer, organizations should continuously refine policies and remove unused access. The new context keys are especially useful for distinguishing AI-driven actions from direct user actions in those policies.

### Addressing security and compliance requirements

For customers with strict governance or regulatory requirements, future VPC endpoint support will be an important option because it enables private communication paths in addition to IAM-based restrictions.

### Starting small and refining over time

AWS recommends starting with a deployment pattern that fits current needs, beginning with **restrictive IAM policies**, and then gradually relaxing permissions as teams better understand what their AI agents actually need to do. The post also recommends using **CloudTrail logs** to monitor what actions AI agents perform in practice. That audit data can then be used to iteratively improve IAM policies over time.

---

## Conclusion

This AWS Security Blog post presents an important step in making AI-assisted development on AWS both practical and governable. By introducing the standardized IAM context keys **`aws:ViaAWSMCPService`** and **`aws:CalledViaAWSMCP`**, AWS gives organizations the ability to distinguish between **human-driven** and **AI-driven** actions while continuing to rely on the IAM model they already use and trust.

The post also shows that AWS is simplifying the public endpoint authorization model so AWS-managed MCP servers work more like familiar tools such as the AWS CLI and SDKs. This reduces the need for separate MCP-specific permissions and allows administrators to focus on managing access at the service level. Looking ahead, planned **VPC endpoint support** will add another valuable layer of control for organizations that need stronger network isolation and perimeter-based protections.

Overall, the approach described in the blog helps organizations adopt AI agents in AWS development workflows without giving up the policy consistency, governance, and auditability that are essential for secure cloud operations.

---

## About the Authors

**Riggs Goodman III** is a Principal Partner Solution Architect at AWS. His current focus is on AI security and networking, where he provides technical guidance, architecture patterns, and leadership to help customers and partners build AI workloads on AWS. Internally, he also helps drive technical strategy and innovation across AWS service teams to address customer and partner challenges.

**Praneeta Prakash** is a Senior Product Manager at AWS Developer Tools. She works at the intersection of cloud infrastructure and developer experience, leading strategic initiatives that shape how developers interact with cloud systems, especially in the growing world of AI-native development. Her work focuses on making AWS more accessible and intuitive for developers at all levels.

**Khaled Sinno** is a Principal Engineer at Amazon Web Services. His current work centers on Identity and Access Management in AWS and broader security and identity controls in the cloud. Previously, he worked on availability and security in AWS RDS and contributed more broadly to the security of database and search services. Before joining AWS, he led large engineering teams in the FinTech industry, working on distributed systems for finance and trading platforms.

**Shreya Jain** is a Senior Technical Product Manager in AWS Identity. She is passionate about making complex ideas clearer and simpler. Outside of work, she enjoys Pilates, dancing, and exploring new coffee shops.