# Graphite module for Icinga Web 2

## General Information

Enable the graphite carbon cache writer: http://docs.icinga.org/icinga2/latest/doc/module/icinga2/chapter/monitoring-basics#graphite-carbon-cache-writer

All perfdata metrics will be automatically included as graphs however if you just want a subset, the host or service then needs to have custom vars of the form vars.graphite_keys =["key1","key2"] where key1 key2 represent perfdata stats you want to see.

You can configure the graphite metric keys formats by using standard-ish icinga2 macros.
## Installation

Just extract this to your Icinga Web 2 module folder in a folder called graphite.

(Configuration -> Modules -> graphite -> enable). Check the modules config tab right there.

NB: It is best practice to install 3rd party modules into a distinct module
folder like /usr/share/icingaweb2/modules. In case you don't know where this
might be please check the module path in your Icinga Web 2 configuration.

##Configuration
There are various configuration settings to tweak how the module behaves and ensure that it aligns with how the graphite carbon cache writer is set up:

``base_url``
A fully formed url 
* *http://graphite.com/render?*

``legacy_mode``
To support older versions of the writer pre-icinga2 2.4 where true - is replaced with _ 
* *false*

``service_name_template``
Macro template for the service name 
* *$host.name$.services.$service.name$.$service.check_command$.perfdata*

``host_name_template``
Macro template for the host name 
* *$host.name$.host.$host.check_command$.perfdata*

``graphite_args_template ``
Macro template for the small image where $target$ is replaced with the metric name 
* *&target=$target$.value&source=0&width=300&height=120&hideAxes=true&lineWidth=1&hideLegend=true&colorList=049BAF&lineMode=connected*

``graphite_large_args_template ``
Macro template for the large image 
* *&target=alias(color($target$.warn,'yellow'),'warning')&target=alias(color($target$.crit,'red'),'critical')&target=$target$.value&source=0&width=800&height=700&colorList=049BAF&lineMode=connected*

``remote_fetch``
To allow remote fetch of the graph image. Useful in multi-tenant installations and/or with password protected graphite-web installations (http auth).
Set base_url as http://user:pass@graphite.com/render?
* *false*

``remote_verify_peer``
Verify remote peer certificate (if using https base_url)
* *false*

``remote_verify_peer_name``
Verify remote peer common name in certificate (if using https base_url)
* *false*

## Hats off to

This module borrows a lot from https://github.com/Icinga/icingaweb2-module-pnp4nagios

## What it looks like		

![screen shot of graphite graph](https://raw.githubusercontent.com/philiphoy/icingaweb2-module-graphite/master/Capture.PNG)
