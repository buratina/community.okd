# OKD/OpenShift Collection for Ansible

[![CI](https://github.com/ansible-collections/community.okd/workflows/CI/badge.svg?event=push)](https://github.com/ansible-collections/community.okd/actions) [![Codecov](https://img.shields.io/codecov/c/github/ansible-collections/community.okd)](https://codecov.io/gh/ansible-collections/community.okd)

This repo hosts the `community.okd` Ansible Collection.

The collection includes a variety of Ansible content to help automate the management of applications in OKD/OpenShift clusters, as well as the provisioning and maintenance of clusters themselves.

## Included content

Click on the name of a plugin or module to view that content's documentation:

  - **Inventory Source**:
    - [openshift](https://docs.ansible.com/ansible/2.10/collections/community/kubernetes/openshift_inventory.html)

## Installation and Usage

### Installing the Collection from Ansible Galaxy

Before using the OKD collection, you need to install it with the Ansible Galaxy CLI:

    ansible-galaxy collection install community.okd

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: community.okd
    version: 0.1.0
```

### Installing the OpenShift Python Library

Content in this collection requires the [OpenShift Python client](https://pypi.org/project/openshift/) to interact with Kubernetes' APIs. You can install it with:

    pip3 install openshift

### Using modules from the OKD Collection in your playbooks

It's preferable to use content in this collection using their Fully Qualified Collection Namespace (FQCN), for example `community.okd.openshift`:

```yaml
---
plugin: community.okd.openshift
connections:
  - namespaces:
    - testing
```

For documentation on how to use individual plugins included in this collection, please see the links in the 'Included content' section earlier in this README.

## Testing and Development

If you want to develop new content for this collection or improve what's already here, the easiest way to work on the collection is to clone it into one of the configured [`COLLECTIONS_PATHS`](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#collections-paths), and work on it there.

### Testing with `ansible-test`

The `tests` directory contains configuration for running sanity and integration tests using [`ansible-test`](https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html).

You can run the collection's test suites with the commands:

    ansible-test sanity --docker -v --color
    ansible-test integration --docker -v --color

## Publishing New Versions

The current process for publishing new versions of the OKD Collection is manual, and requires a user who has access to the `community.okd` namespace on Ansible Galaxy to publish the build artifact.

  1. Ensure you're running Ansible from devel, so the [`build_ignore` key](https://github.com/ansible/ansible/issues/67130) in `galaxy.yml` is used.
  1. Run `git clean -x -d -f` in this repository's directory to clean out any extra files which should not be included.
  1. Update `galaxy.yml` and this README's `requirements.yml` example with the new `version` for the collection.
  1. Update the CHANGELOG:
    1. Make sure you have [`antsibull-changelog`](https://pypi.org/project/antsibull-changelog/) installed.
    1. Make sure there are fragments for all known changes in `changelogs/fragments`.
    1. Run `antsibull-changelog release`.
  1. Commit the changes and create a PR with the changes. Wait for tests to pass, then merge it once they have.
  1. Tag the version in Git and push to GitHub.
  1. Run the following commands to build and release the new version on Galaxy:

     ```
     ansible-galaxy collection build
     ansible-galaxy collection publish ./community-okd-$VERSION_HERE.tar.gz
     ```

After the version is published, verify it exists on the [OKD Collection Galaxy page](https://galaxy.ansible.com/community/okd).

## More Information

For more information about Ansible's Kubernetes and OpenShift integrations, join the `#ansible-kubernetes` channel on Freenode IRC, and browse the resources in the [Kubernetes Working Group](https://github.com/ansible/community/wiki/Kubernetes) Community wiki page.

## License

GNU General Public License v3.0 or later

See LICENCE to see the full text.
