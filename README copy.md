# Ansible Collection: Workspace ONE Cloud Services - SaaS

This repo hosts the `ws1cs.saas` Ansible Collection. The collection includes a variety of custom Ansible roles specific to SaaS.

## Included Content

The following plugins and roles are included:

- **Roles**:
  - saas_cps_files
  - saas_cps_service
  - saas_image_prep
  - saas_linux_configure
  - sde_ansible
  - sde_jenkins
  - sde_powercli

### Using roles or modules from this collection in your playbooks

You can call roles & modules by their short name if you list the `ws1cs.saas` collection in the playbook's `collections`, like so:

```yaml
---
- hosts: servers
  collections:
    - ws1cs.saas
  tasks:
    - name: Add Server to SaaSWatch
      awsw_server:
        solarwinds_server: "{{ solarwinds_server }}"
        username: "{{ ansible_user }}@{{ admin_domain | upper }}"
        password: "{{ ansible_password }}"
        is_airwatch_upgrade: true

- hosts: servers
  collections:
    - ws1cs.saas
  roles:
    - domain_join
```

You can also call modules by their Fully Qualified Collection Namespace (FQCN), like `ws1cs.saas.module_name`:

```yaml
---
- hosts: servers
  tasks:
    - name: Add Server to SaaSWatch
      ws1cs.saas.awsw_server:
        solarwinds_server: "{{ solarwinds_server }}"
        username: "{{ ansible_user }}@{{ admin_domain | upper }}"
        password: "{{ ansible_password }}"
        is_airwatch_upgrade: true

- hosts: servers
  roles:
    - ws1cs.saas.domain_join
```

For documentation on how to use individual modules and other content included in this collection, please see the links in the 'Included content' section earlier in this README.

## Testing and Development

If you want to develop new content for this collection or improve what's already here, the easiest way to work on the collection is to clone it into one of the configured [`COLLECTIONS_PATHS`](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#collections-paths), and work on it there.

### Testing with `ansible-test`

The `tests` directory contains configuration for running sanity and integration tests using [`ansible-test`](https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html).

### Continous Integration

Before a successful merge to main, contributors must pass several quality gates enforced by CI. All PR's must be submitted to the `staging` branch. Upon successful approval, `staging` will be automatically merged to main once a full series of integration tests have been run.

### Build Process

Artifacts are generated on every commit and published to the EUC Artifactory instance.

    {namespace}-{name}-{version}-{commit/latest}.tar.gz

The actual artifact name is constructed based on the `namespace`, `name`, `version` and `commit`.

    {namespace}-{name}-{version}-latest.tar.gz

A second artifact is generated with the name `latest` appended instead of the commit hash. This represents the latest build for that version.

`https://artifactory.air-watch.com/artifactory/euc-cloudops/collections/{namespace}/{name}/`

Artifacts are uploaded to the `euc-cloudops` repository in Artifactory in the above format, with the aformentioned Artifact.

### Unit Testing

All pull requests with new modules must also submit an associated unit tests. Exemptions will be considered on a case-by-case basis.

Unit tests can be run locally: `make test T="2.10/units/3.7` - this would run unit tests with Ansible 2.10 and Python 3.7.

### Integration Testing

All pull requests with new modules must also submit associated integration tests. Exemptions will be considered on a case-by-case basis. With Ansible plugins, integration tests are written as Ansible roles.

Integration tests can be run locally: `make test T="2.10/integration/3.7/centos8` - this would run integration tests in a CentOS 8 environment with Ansible 2.10 and Python 3.7.

### Windows Integration Testing

All pull requests with new modules must also submit associated integration tests. Exemptions will be considered on a case-by-case basis. With Ansible plugins, integration tests are written as Ansible roles.

Windows Integration tests can be run locally: `make test T="2.10/wintegration/2019` - this would run Windows integration tests in a Windows Server 2019 Core environment with Ansible 2.10.

## More Information

Pending.

## License

N/A - Internal Use
