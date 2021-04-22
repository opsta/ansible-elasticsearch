# Ansible Role: Elasticsearch

This role can install in different node configuration:
- Standalone
- Cluster
  - All in one node
  - Master node
  - Data node
  - Client node

Also with various configuration:
- SSL encryption
- License activation

## Requirements

- If you install with SSL HTTP enabled. The target hosts will need to have **full FQDN*** set. Otherwise both change password and activate license task will fail since it require domain to connect. I have already updated inventory example in description.

## Role Variables

- `elasticsearch_data_path`: Specified data path
- `elasticsearch_log_path`: Specified log path
- `elasticsearch_http_port`: Specified HTTP port
- `elasticsearch_transport_port`: Specified range of transport ports
- `elasticsearch_host_license_file_path`: Specified your license file in playbook folder (optional)
- `elasticsearch_ssl_enabled`: Enable/disable SSL encryption (Optional)
- `elasticsearch_ssl_transport_enabled`: Enable/disable transport SSL encryption
- `elasticsearch_ssl_http_enabled`: Enable/disable HTTP SSL encryption
- `elasticsearch_host_ssl_key_file_path`: Specified your private key file in playbook folder
- `elasticsearch_host_ssl_cert_file_path`: Specified your certificate file in playbook folder
- `elasticsearch_host_ssl_ca_file_path`: Specified your CA file in playbook folder
- `elasticsearch_data_path`: Specified data path
- `elasticsearch_log_path`: Specified log path
- `elasticsearch_password`: Sepcified password for elastic default username
- `elasticsearch_min_heap_size`: Minimum java heap size
- `elasticsearch_max_heap_size`: Maximum java heap size

## Dependencies

- https://github.com/opsta/ansible-java

## Example Inventory

- Standalone
```ini
[elasticsearch]
elasticsearch ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
```
- All in one cluster
```ini
elasticsearch-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-3 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22

[elasticsearch]
elasticsearch-1
elasticsearch-2
elasticsearch-3
```
- Multiple roles cluster
```ini
elasticsearch-master-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-3 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
kibana ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22

[elasticsearch_master]
elasticsearch-master-1
elasticsearch-master-2
elasticsearch-master-3

[elasticsearch_data]
elasticsearch-data-1
elasticsearch-data-2

[elasticsearch_client]
kibana
```
- Adding storage tier attribute to node
```ini
elasticsearch-master-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-master-3 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-1 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-2 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22
elasticsearch-data-3 ansible_user=ubuntu ansible_host=x.x.x.x ansible_port=22

[elasticsearch_hot]
elasticsearch-data-1

[elasticsearch_warm]
elasticsearch-data-2

[elasticsearch_cold]
elasticsearch-data-3
```

**Remark:** If you install with SSL HTTP enabled. The target hosts will need to have **full FQDN**. Otherwise both change password and activate license task will fail since it require domain to connect.

## Example Playbook
```yaml
    - hosts: all
      roles:
        - ansible-elasticsearch
```

## License

MIT

## Author Information

Opsta (Thailand) Co.,Ltd.
