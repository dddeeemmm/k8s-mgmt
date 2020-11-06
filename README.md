k8s-mgmt
=========

    Manage Kubernetes content

Requirements
------------

    Kubernetes

Role Variables
--------------

    k8s_mgmt_registry_custom:                    | default: true                        | use docker login
    k8s_mgmt_patch_deployment:                   | default: false                       | force recreate pods     
    k8s_mgmt_image_name:                         | required                             | image name
    k8s_mgmt_image_tag:                          | default: latest                      | image tag  image tag
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_ns:                                 | default: tmp                         | work namespace name    
    k8s_mgmt_ns_state:                           | default: present                     | work namespace state
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_app_group:                          | required                             | folders contain tasks and vars
    k8s_mgmt_app_name:                           | required                             | name of tasks and vars files, app name in k8s
    k8s_mgmt_app_state:                          | default: present                     | deployment state
    k8s_mgmt_app_replicas:                       | default: 1                           | replicas
    k8s_mgmt_app_min_replicas:                   | not required                         | hpa minimal replicas
    k8s_mgmt_app_max_replicas:                   | default: k8s_mgmt_app_replicas       | hpa maximal replicas
    k8s_mgmt_app_cpu_target_average_utilization: | default: 90                          | hpa target cpu utilization
    k8s_mgmt_app_memory_target_average_value:    | not required                         | hpa target memory value
    k8s_mgmt_app_revision_history_limit:         | default: 10                          | revision history limit
    k8s_mgmt_app_rolling_update_partition:       | default: 0                           | rolling update partition
    k8s_mgmt_app_rolling_update_max_surge:       | default: 1                           | rolling update max surge
    k8s_mgmt_app_rolling_update_max_unavailable: | default: 1                           | rolling update max unavailable
    k8s_mgmt_app_request_memory:                 | default: 256Mi                       | request app memory 
    k8s_mgmt_app_request_cpu:                    | default: 256m                        | request app cpu
    k8s_mgmt_app_limit_memory:                   | default: k8s_mgmt_app_request_memory | limit app memory
    k8s_mgmt_app_limit_cpu:                      | default: k8s_mgmt_app_request_cpu    | limit app cpu
    k8s_mgmt_app_port:                           | required                             | app port
    k8s_mgmt_app_probe_initial_delay_seconds:    | default: 30                          | live and ready probe delay
    k8s_mgmt_app_probe_period_seconds:           | default: 10                          | live and ready probe period
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_service_name:                       | default: k8s_mgmt_app_name           | service name
    k8s_mgmt_service_port:                       | required                             | service port
    k8s_mgmt_service_state:                      | default: k8s_mgmt_app_state          | service state
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_configmap:                          | not required                         | configmap content
    k8s_mgmt_configmap_name:                     | default: k8s_mgmt_app_name           | configmap name
    k8s_mgmt_configmap_state:                    | default: k8s_mgmt_app_state          | configmap state
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_deployment_name:                    | default: k8s_mgmt_app_name           | deployment name
    k8s_mgmt_deployment_state:                   | default: k8s_mgmt_app_state          | deployment state
    -----------------------------------------------------------------------------------------------------------------------------------
    k8s_mgmt_hpa_name:                           | default: k8s_mgmt_app_name           | hpa name
    k8s_mgmt_hpa_state:                          | default: k8s_mgmt_app_state          | hpa state

Dependencies
------------

    Kubernetes

Example Playbook
----------------

    - hosts: "{{ groups ['k8s_master'] | random }}"
      become: yes
      vars:
        k8s_mgmt_ns: main
        k8s_mgmt_app_group: group
        k8s_mgmt_app_name: app
        k8s_mgmt_image_name: registry.domain.pro/group/app
        k8s_mgmt_image_tag: 0.0.1
      roles:
        - { name: k8s-mgmt, tags: k8s }

License
-------

    MIT

Author Information
------------------

    Dmitrij Petrov
