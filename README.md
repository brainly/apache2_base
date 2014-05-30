apache2_base
========

This role provides a bare Apache2 installation on Debian Wheeze systems.
PHP may be installed as well, if *apache2_base_php_enabled* flag is set to true.

[![Build Status](https://travis-ci.org/brainly/apache2_base.svg?branch=master)](https://travis-ci.org/brainly/apache2_base)

Requirements
------------

The role requires Ansible 1.6 and higher due to dependency on apache2_module.
All the platform requirements are listed in the metadata file.

Role Variables
--------------

Below is a list of variables that are available:

Apache server related:
- *apache2_base_extra_packages*: additionall Apache2 related packages that should be
    installed by the role
- *apache2_base_extra_modules*: additionall Apache2 module configuration files that
    should be enabled
- *apache2_base_host*: host part of the Apache2's *Listen* directive
- *apache2_base_port*: port part of the Apache2's *Listen* directive
- *apache2_base_ssl_port*: port part of the Apache2's *Listen* directive for incomming
    SSL connnections
- *apache2_base_prefork_start_servers*: Apache2's *StartServers* directive
- *apache2_base_prefork_min_spare_servers*: Apache2's *MinSpareServers* directive
- *apache2_base_prefork_max_spare_servers*: Apache2's *MaxSpareServers* directive
- *apache2_base_prefork_max_clients*: Apache2's *MaxClients* directive
- *apache2_base_prefork_max_requests_per_child*: Apache2's *MaxRequestsPerChild*
    directive
- *apache2_base_connection_timeout*: Apache2's *Timeout* directive
- *apache2_base_keepalive*: Apache2's *KeepAlive* directive
- *apache2_base_keepalive_max_requests*: Apache2's *KeepAliveTimeout* directive, included
     only if *apache2_base_keepalive* is set to "On"
- *apache2_base_keepalive_timeout*: Apache2's *KeepAliveTimeout* directive, included only
    if *apache2_base_keepalive* is set to "On"
- *apache2_base_rpafproxy_ips*: list of source IPs that RPAF module (if
  enabled) will treat as trusted

modphp related:
- *apache2_base_php_enabled* - if set to True PHP will be installed and configured
- *apache2_base_php_extra_packages*, *apache2_base_php_max_execution_time*, *apache2_base_php_post_max_size*,
    *apache2_base_php_upload_max_filesize*, *apache2_base_php_memory_limit*, *apache2_base_php_file_uploads*,
    *apache2_base_php_short_open_tag*: values of all these directives are used as-is while
    determining the value of their php.ini's counterparts.
- *apache2_base_php_timezone*: translates directly to php.ini's *date.timezone* directive
- *apache2_base_php_open_basedir*: list elements are joined and used as a value for php.ini's
    *open_basedir* directive

php.ini's *disable_functions* option has more complex configuration. There are three
    role variables which relate to it:
- *apache2_base_php_disabled_functions*: it provides global set of foribiden PHP functions. The
    only case when it should have group/host specific override is when the set of
    disabled funcitions is radically different (or none).
- *apache2_base_php_reenabled_functions*: in case when a website/host group/host needs an exception,
    this list allows to reenable only particular function/functions. Use with care!
- *apache2_base_php_extra_disabled_functions*: should be used when there is a need for extra security
    for given group/ website/host and some additionall PHP functions should be disabled.

Please see defaults/main.yml for example values of some of mentioned variables.

All variables have sane defaults, so defining them is optional.

Dependencies
------------

Role requires at least one additionall role that will provide vhost configuration
and content to serve. Please check apache2_examplehost role for more details.
This role alone will not produce usable HTTP server.

Example Playbook
-------------------------

Applying the role is straightforward:

```
- hosts: www-servers
  roles:
    - apache2_base
    - apache2_examplehost
```

License
-------

Copyright 2014 Zadane.pl sp. z o.o.

Copyright 2014 Pawel Rozlach

Copyright 2013 Andrew Smith

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this role except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Author Information
------------------

The idea for this role and some of its parts come from Andrew Smith's apache2-vhosts
role:

https://github.com/EspadaV8/ansible-apache2-vhosts.git

licensed under MIT license. It has been adapted and extended to match Zadane.pl's
requirements by Pawel Rozlach during the work time and spare time and then
opensourced by the company.

Some important contributions and fixes have also been made by Rafał Trójniak
(https://github.com/rafaltrojniak) and Jakub Kramarz (https://github.com/jkramarz).
