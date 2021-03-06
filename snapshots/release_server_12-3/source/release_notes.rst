
=====================================================
Release Notes: Chef Server 12.3
=====================================================

.. tag chef_index

Chef is a systems and cloud infrastructure automation framework that makes it easy to deploy servers and applications to any physical, virtual, or cloud location, no matter the size of the infrastructure. Each organization is comprised of one (or more) workstations, a single server, and every node that will be configured and maintained by the chef-client. Cookbooks (and recipes) are used to tell the chef-client how each node in your organization should be configured. The chef-client (which is installed on every node) does the actual configuration.

.. end_tag

What's New
=====================================================
The following items are new for Chef server 12.3:

* **Nginx stub_status module is enabled** The Nginx ``stub_status`` module is enabled by default and may be viewed at the ``/nginx_status`` endpoint. The settings for this module are configurable.
* **RabbitMQ queue tuning** New settings for managing RabbitMQ queues allow the size of the queue used by Chef Analytics to be configured, including settings for the queue length monitor and for tuning the rabbitmq-management plugin.

Nginx stub_status Module
-----------------------------------------------------
The following configuration settings are new and enable the Nginx ``stub_status`` module:

``nginx['enable_stub_status']``
   Enables the Nginx ``stub_status`` module. See ``nginx['stub_status']['allow_list']``, ``nginx['stub_status']['listen_host']``, ``nginx['stub_status']['listen_port']``, and ``nginx['stub_status']['location']``. Default value: ``true``.

``nginx['stub_status']['allow_list']``
   The IP address on which accessing the ``stub_status`` endpoint is allowed. Default value: ``["127.0.0.1"]``.

``nginx['stub_status']['listen_host']``
   The host on which the Nginx ``stub_status`` module listens. Default value: ``"127.0.0.1"``.

``nginx['stub_status']['listen_port']``
   The port on which the Nginx ``stub_status`` module listens. Default value: ``"9999"``.

``nginx['stub_status']['location']``
   The name of the Nginx ``stub_status`` endpoint used to access data generated by the Nginx ``stub_status`` module. Default value: ``"/nginx_status"``.

RabbitMQ Queues
-----------------------------------------------------
.. tag server_tuning_rabbitmq_analytics_queue

If the RabbitMQ queue that is used by Chef Analytics stops consuming messages, the Chef server data partition will fill up and may affect the overall performance of the Chef server application itself. The settings for the RabbitMQ queue are tunable, including for queue length monitoring, queue capacity, maximum number of messages that can be in the queue before messages are dropped, the point at which messages are dropped, for settings used by the rabbitmq-management plugin, and so on.

.. end_tag

.. tag server_tuning_rabbitmq_analytics_queue_settings

The following settings may be used for tuning RabbitMQ queues used by Chef Analytics and the Chef server:

``rabbitmq['analytics_max_length']``
   The maximum number of messages that can be queued before RabbitMQ automatically drops messages from the front of the queue to make room for new messages. Default value: ``10000``.

``rabbitmq['drop_on_full_capacity']``
   Specify if messages will stop being sent to the RabbitMQ queue when it is at capacity. Default value: ``true``.

``rabbitmq['management_enabled']``
   Specify if the rabbitmq-management plugin is enabled. Default value: ``true``.

``rabbitmq['management_password']``
   The rabbitmq-management plugin password. Default value: ``'chefrocks'``.

``rabbitmq['management_port']``
   The rabbitmq-management plugin port. Default value: ``15672``.

``rabbitmq['management_user']``
   The rabbitmq-management plugin user. Default value: ``'rabbitmgmt'``.

``rabbitmq['prevent_erchef_startup_on_full_capacity']``
   Specify if the Chef server will start when the monitored RabbitMQ queue is full. Default value: ``false``.

``rabbitmq['queue_at_capacity_affects_overall_status']``
   Specify if the ``_status`` endpoint in the Chef server API will fail if the monitored queue is at capacity. Default value: ``false``.

``rabbitmq['queue_length_monitor_enabled']``
   Specify if the queue length monitor is enabled. Default value: ``true``.

``rabbitmq['queue_length_monitor_millis']``
   The frequency (in milliseconds) at which the length of the RabbitMQ queue is checked. Default value: ``30000``.

``rabbitmq['queue_length_monitor_timeout_millis']``
   The timeout (in milliseconds) at which calls to the queue length monitor will stop if the Chef server is overloaded. Default value: ``5000``.

``rabbitmq['queue_length_monitor_queue']``
   The RabbitMQ queue that is observed by queue length monitor. Default value: ``'alaska'``.

``rabbitmq['queue_length_monitor_vhost']``
   The virtual host for the RabbitMQ queue that is observed by queue length monitor. Default value: ``'/analytics'``.

``rabbitmq['rabbit_mgmt_http_cull_interval']``
   The maximum cull interval (in seconds) for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``60``.

``rabbitmq['rabbit_mgmt_http_init_count']``
   The initial worker count for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``25``.

``rabbitmq['rabbit_mgmt_http_max_age']``
   The maximum connection worker age (in seconds) for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``70``.

``rabbitmq['rabbit_mgmt_http_max_connection_duration']``
   The maximum connection duration (in seconds) for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``70``.

``rabbitmq['rabbit_mgmt_http_max_count']``
   The maximum worker count for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``100``.

``rabbitmq['rabbit_mgmt_ibrowse_options']``
   An array of comma-separated key-value pairs of ibrowse options for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``'{connect_timeout, 10000}'``.

``rabbitmq['rabbit_mgmt_timeout']``
   The timeout for the HTTP connection pool that is used by the rabbitmq-management plugin. Default value: ``30000``.

``rabbitmq['ssl_versions']``
   The SSL versions used by the rabbitmq-management plugin. (See also |url rabbitmqssl|.) Default value: ``['tlsv1.2', 'tlsv1.1']``.

.. end_tag

What's Fixed
=====================================================
For the list of issues that were addressed for this release, please see the changelog on GitHub: https://github.com/chef/chef-server/blob/master/CHANGELOG.md
