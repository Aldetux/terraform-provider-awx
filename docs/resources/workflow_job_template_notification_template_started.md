---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "awx_workflow_job_template_notification_template_started Resource - terraform-provider-awx"
subcategory: ""
description: |-
  Provides a resource for creating a notification template for a workflow job template that will be triggered on started.
---

# awx_workflow_job_template_notification_template_started (Resource)

Provides a resource for creating a notification template for a workflow job template that will be triggered on started.

## Example Usage

```terraform
data "awx_organization" "example" {
  name = "Default"
}

resource "awx_inventory" "example" {
  name            = "Example Inventory"
  organization_id = data.awx_organization.example.id
}

resource "awx_project" "example" {
  name            = "example-ansible-main"
  organization_id = data.awx_organization.example.id
  scm_type        = "git"
  scm_url         = "git@github.com/josh-silvas/example-ansible.git"
  scm_branch      = "main"
}

resource "awx_workflow_job_template" "example" {
  name            = "workflow-job"
  organization_id = data.awx_organization.example.id
  inventory_id    = awx_inventory.example.id
}

resource "awx_job_template" "example" {
  name           = "baseconfig"
  job_type       = "run"
  inventory_id   = awx_inventory.example.id
  project_id     = awx_project.example.id
  playbook       = "master-configure-system.yml"
  become_enabled = true
}

resource "awx_notification_template" "example" {
  name = "notification_template-test"
}

resource "awx_workflow_job_template_notification_template_started" "baseconfig" {
  workflow_job_template_id = awx_workflow_job_template.example.id
  notification_template_id = awx_notification_template.example.id
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `notification_template_id` (Number) The ID of the notification template to associate with the workflow job template.
- `workflow_job_template_id` (Number) The ID of the workflow job template to associate the notification template with.

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
# Order can be imported by specifying the numeric identifier.
terraform import awx_workflow_job_template_notification_template_started.example 860
```