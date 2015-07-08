
This project is a for for: (https://github.com/abtpeople/ansible-elasticsearch)

We add this validation:

1.- 'To validate first if the current plugin to install was installed or not.'
command: bin/plugin -l
when: lstElasticPlugins.stdout.find('{{item.id}}') == -1

Error when we try to install a plugin that is already installed:
plugin -install mobz/elasticsearch-head
-> Installing mobz/elasticsearch-head...
Failed to install mobz/elasticsearch-head, reason: plugin directory C:\dsusanibar\innovation\elk\plugin\head already exists. 
To update the plugin, uninstall it first using --remove mobz/elasticsearch-head command

2.- 'We add an example about how do we could use the role "ansible-elasticsearch".'
ansible-elasticsearch/examples/site_elasticsearch_playbook.yml

- hosts: localhost
  roles:
    - role: ansible-elasticsearch
      es_default_heap_size: 1.5g
      es_etc_cluster_name: cluster_vz_elasticsearch
      es_etc_node_name: node_vz_proofoftechvm8
      es_etc_path_conf: /etc/elasticsearch
      es_etc_path_data: /home/peruhackaton/dsusanibar/elk/data
      es_etc_path_work: /home/peruhackaton/dsusanibar/elk/work
      es_etc_path_logs: /home/peruhackaton/dsusanibar/elk/logs
      es_etc_path_plugins: /home/peruhackaton/dsusanibar/elk/plugins
      es_etc_http_port: 8010
      #es_etc_node_master: true
      #es_etc_node_data: true
      es_plugins:
        - name: mobz/elasticsearch-head
          url: http://mobz.github.io/elasticsearch-head/archive/mmaster.zip
          id: head
        - name: karmi/elasticsearch-paramedic
          url: https://github.com/karmi/elasticsearch-paramedic/archive/master.zip
          id: paramedic
        - name: royrusso/elasticsearch-HQ
          url: https://github.com/royrusso/elasticsearch-HQ/archive/master.zip
          id: HQ
