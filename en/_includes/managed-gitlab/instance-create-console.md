{% note warning %}

Once an instance is created, you cannot change its resource configuration, i.e., instance type, disk size, and availability zone.

{% endnote %}

1. In the management console, select the [folder](../../resource-manager/concepts/resources-hierarchy.md#folder) where you want to create a [{{ GL }} instance](../../managed-gitlab/concepts/index.md#instance).
1. Select **{{ ui-key.yacloud.iam.folder.dashboard.label_managed-gitlab }}**.
1. Click **{{ ui-key.yacloud.gitlab.button_create-instance }}**.
1. Under **{{ ui-key.yacloud.compute.group.overview.section_base }}**:

   1. Enter the instance name. It must be unique throughout {{ yandex-cloud }}.

      {% include [name-format](../name-format.md) %}

   1. (Optional) Enter a description of the instance.

1. Under **{{ ui-key.yacloud.gitlab.label_configuration-section }}**:

   1. Select the instance type.
   1. Specify the [subnet](../../vpc/concepts/network.md#subnet) where the instance will be hosted. Currently, you cannot select a subnet with the `192.168.0.0/24` address range due to {{ yandex-cloud }} technical restrictions.

      The [default security group](../../vpc/concepts/security-groups.md#default-security-group) for the selected [network](../../vpc/concepts/network.md#network) will be used for the instance. If you cannot open the {{ GL }} web interface after creating the instance, create a separate security group and [configure it](../../managed-gitlab/operations/configure-security-group.md) so that the rules allow incoming traffic from the required ports and IP addresses.

   1. Select the [disk](../../compute/concepts/disk.md) size.
   1. Specify the [instance domain name](../../compute/concepts/network.md#hostname): the required DNS records for this domain name will be automatically created in `.gitlab.yandexcloud.net`.

      The domain name must be unique throughout {{ yandex-cloud }}.

      * Its length must be between 5 and 50 characters.
      * It may contain lowercase Latin letters, numbers, and hyphens.
      * It must not start or end with a dash character.

   1. Set up the retention period for automatic backups (in days).
   1. (Optional) Enable [code approval rules](../../managed-gitlab/concepts/approval-rules.md). To do this, select the appropriate configuration for approval rules.

      {% include [note-approval-rules-pricing](note-approval-rules-pricing.md) %}

1. Under **{{ ui-key.yacloud.gitlab.label_admin-section }}**, specify:
   * **{{ ui-key.yacloud.gitlab.field_admin-email }}**: Email address of the {{ GL }} instance administrator. This mailbox will receive an email with a link for creating a password.
   * **{{ ui-key.yacloud.gitlab.field_admin-login }}**: Administrator login.
1. Click **{{ ui-key.yacloud.common.create }}**.
1. Wait for the instance to get ready: its status on the {{ mgl-name }} dashboard will change to **Running**. This may take some time.
