# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`chrony`](#chrony): Installs and configures chrony

#### Private Classes

* `chrony::config`: Configures chrony
* `chrony::install`: Installs chrony
* `chrony::service`: Manages the chrony service

### Functions

#### Private Functions

* `chrony::server_array_to_hash`: Function to normalise servers/pools/peers

### Data types

* [`Chrony::Servers`](#Chrony--Servers): Type for the `servers`, `pools` and `peers` parameters.

## Classes

### <a name="chrony"></a>`chrony`

Installs and configures chrony

* **See also**
  * https://chrony.tuxfamily.org

#### Examples

##### Install chrony with default options

```puppet
include chrony
```

##### Use specific servers (These will be configured with the `iburst` option.)

```puppet
class { 'chrony':
  servers => [ 'ntp1.corp.com', 'ntp2.corp.com', ],
}
```

##### Two specific servers without `iburst`

```puppet
class { 'chrony':
  servers => {
    'ntp1.corp.com' => [],
    'ntp2.corp.com' => [],
  },
}
```

##### Ensure a secret password is used for chronyc

```puppet
class { 'chrony':
  servers         => [ 'ntp1.corp.com', 'ntp2.corp.com', ],
  chrony_password => 'secret_password',
}
```

##### Use NTP authentication

```puppet
class { 'chrony':
  keys            => [
    '25 SHA1 HEX:1dc764e0791b11fa67efc7ecbc4b0d73f68a070c',
  ],
  servers         => {
    'ntp1.corp.com' => ['key 25', 'iburst'],
    'ntp2.corp.com' => ['key 25', 'iburst'],
  },
}
```

##### Have chronyd autogenerate a command key at startup

```puppet
class { 'chrony':
  chrony_password    => 'unset',
  config_keys_manage => false,
}
```

##### Allow some hosts

```puppet
class { 'chrony':
  queryhosts => ['192.168/16'],
}
```

##### Configure the leap second mode

```puppet
class { 'chrony':
  leapsecmode => 'slew',
  smoothtime  => '400 0.001 leaponly',
  maxslewrate => 1000.0
}
```

##### Configure [makestep](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#makestep)

```puppet
# Step the system clock if the adjustment is larger than 1000 seconds, but only in the first ten clock updates.
class { 'chrony':
  makestep_seconds => 1000,
  makestep_updates => 10,
}
```

#### Parameters

The following parameters are available in the `chrony` class:

* [`bindaddress`](#-chrony--bindaddress)
* [`bindcmdaddress`](#-chrony--bindcmdaddress)
* [`initstepslew`](#-chrony--initstepslew)
* [`confdir`](#-chrony--confdir)
* [`sourcedir`](#-chrony--sourcedir)
* [`cmdacl`](#-chrony--cmdacl)
* [`cmdport`](#-chrony--cmdport)
* [`commandkey`](#-chrony--commandkey)
* [`chrony_password`](#-chrony--chrony_password)
* [`config`](#-chrony--config)
* [`config_template`](#-chrony--config_template)
* [`config_keys`](#-chrony--config_keys)
* [`config_keys_manage`](#-chrony--config_keys_manage)
* [`config_keys_template`](#-chrony--config_keys_template)
* [`config_keys_owner`](#-chrony--config_keys_owner)
* [`config_keys_group`](#-chrony--config_keys_group)
* [`config_keys_mode`](#-chrony--config_keys_mode)
* [`keys`](#-chrony--keys)
* [`driftfile`](#-chrony--driftfile)
* [`local_stratum`](#-chrony--local_stratum)
* [`local_orphan`](#-chrony--local_orphan)
* [`ntpsigndsocket`](#-chrony--ntpsigndsocket)
* [`stratumweight`](#-chrony--stratumweight)
* [`log_options`](#-chrony--log_options)
* [`logbanner`](#-chrony--logbanner)
* [`logchange`](#-chrony--logchange)
* [`package_ensure`](#-chrony--package_ensure)
* [`package_name`](#-chrony--package_name)
* [`package_source`](#-chrony--package_source)
* [`package_provider`](#-chrony--package_provider)
* [`peers`](#-chrony--peers)
* [`servers`](#-chrony--servers)
* [`pools`](#-chrony--pools)
* [`minsources`](#-chrony--minsources)
* [`minsamples`](#-chrony--minsamples)
* [`refclocks`](#-chrony--refclocks)
* [`makestep_seconds`](#-chrony--makestep_seconds)
* [`makestep_updates`](#-chrony--makestep_updates)
* [`queryhosts`](#-chrony--queryhosts)
* [`denyqueryhosts`](#-chrony--denyqueryhosts)
* [`port`](#-chrony--port)
* [`service_enable`](#-chrony--service_enable)
* [`service_ensure`](#-chrony--service_ensure)
* [`service_manage`](#-chrony--service_manage)
* [`service_name`](#-chrony--service_name)
* [`wait_enable`](#-chrony--wait_enable)
* [`wait_ensure`](#-chrony--wait_ensure)
* [`wait_manage`](#-chrony--wait_manage)
* [`wait_name`](#-chrony--wait_name)
* [`smoothtime`](#-chrony--smoothtime)
* [`mailonchange`](#-chrony--mailonchange)
* [`threshold`](#-chrony--threshold)
* [`lock_all`](#-chrony--lock_all)
* [`sched_priority`](#-chrony--sched_priority)
* [`leapsecmode`](#-chrony--leapsecmode)
* [`leapsectz`](#-chrony--leapsectz)
* [`maxdistance`](#-chrony--maxdistance)
* [`maxslewrate`](#-chrony--maxslewrate)
* [`ntsserverkey`](#-chrony--ntsserverkey)
* [`ntsservercert`](#-chrony--ntsservercert)
* [`ntsport`](#-chrony--ntsport)
* [`maxntsconnections`](#-chrony--maxntsconnections)
* [`ntsprocesses`](#-chrony--ntsprocesses)
* [`ntsdumpdir`](#-chrony--ntsdumpdir)
* [`ntsntpserver`](#-chrony--ntsntpserver)
* [`ntsrotate`](#-chrony--ntsrotate)
* [`clientlog`](#-chrony--clientlog)
* [`clientloglimit`](#-chrony--clientloglimit)
* [`rtcsync`](#-chrony--rtcsync)
* [`rtconutc`](#-chrony--rtconutc)
* [`hwtimestamps`](#-chrony--hwtimestamps)
* [`dumpdir`](#-chrony--dumpdir)
* [`maxupdateskew`](#-chrony--maxupdateskew)
* [`acquisitionport`](#-chrony--acquisitionport)

##### <a name="-chrony--bindaddress"></a>`bindaddress`

Data type: `Array[Stdlib::IP::Address]`

Array of addresses of interfaces on which chronyd will listen for NTP traffic.
Listens on all addresses if left empty.

Default value: `[]`

##### <a name="-chrony--bindcmdaddress"></a>`bindcmdaddress`

Data type: `Array[String]`

Array of addresses of interfaces on which chronyd will listen for monitoring command packets.

Default value: `['127.0.0.1', '::1']`

##### <a name="-chrony--initstepslew"></a>`initstepslew`

Data type: `Optional[String]`

Allow chronyd to make a rapid measurement of the system clock error at boot time,
and to correct the system clock by stepping before normal operation begins.

Default value: `undef`

##### <a name="-chrony--confdir"></a>`confdir`

Data type: `Optional[Stdlib::Absolutepath]`

The confdir directive includes configuration files with the .conf suffix from a directory.

Default value: `undef`

##### <a name="-chrony--sourcedir"></a>`sourcedir`

Data type: `Optional[Stdlib::Absolutepath]`

The sourcedir directive is identical to the confdir directive, except the configuration files have the .sources suffix, they can only specify NTP sources.

Default value: `undef`

##### <a name="-chrony--cmdacl"></a>`cmdacl`

Data type: `Array[String]`

An array of ACLs for monitoring access. This expects a list of directives, for
example: `['cmdallow 1.2.3.4', 'cmddeny 1.2.3']`. The order will be respected at
the time of generating the configuration. The argument of the allow or deny
commands can be an address, a partial address or a subnet (see manpage for more
details).

Default value: `[]`

##### <a name="-chrony--cmdport"></a>`cmdport`

Data type: `Optional[Stdlib::Port]`

The cmdport directive allows the port that is used for run-time monitoring (via the chronyc program)
to be altered from its default (323).

Default value: `undef`

##### <a name="-chrony--commandkey"></a>`commandkey`

Data type: `NotUndef`

This sets the key ID used by chronyc to authenticate to chronyd.

Default value: `0`

##### <a name="-chrony--chrony_password"></a>`chrony_password`

Data type: `Variant[Sensitive[String[1]], String[1]]`

This sets the chrony password to be used in the key file.
By default a short fixed string is used. If set explicitly to
'unset' then no password will be added to the keys file by puppet.

Default value: `'xyzzy'`

##### <a name="-chrony--config"></a>`config`

Data type: `Stdlib::Unixpath`

This sets the file to write chrony configuration into.

Default value: `'/etc/chrony/chrony.conf'`

##### <a name="-chrony--config_template"></a>`config_template`

Data type: `String[1]`

This determines which template puppet should use for the chrony configuration.

Default value: `'chrony/chrony.conf.epp'`

##### <a name="-chrony--config_keys"></a>`config_keys`

Data type: `Variant[Stdlib::Unixpath,String[0,0]]`

This sets the file to write chrony keys into. Set to '' to remove `keyfile` attribute from the config.

Default value: `'/etc/chrony/chrony.keys'`

##### <a name="-chrony--config_keys_manage"></a>`config_keys_manage`

Data type: `Boolean`

Determines whether puppet will manage the content of the keys file after it has been created for the first time.

Default value: `true`

##### <a name="-chrony--config_keys_template"></a>`config_keys_template`

Data type: `String[1]`

This determines which template puppet should use for the chrony key file.

Default value: `'chrony/chrony.keys.epp'`

##### <a name="-chrony--config_keys_owner"></a>`config_keys_owner`

Data type: `Variant[Integer[0],String[1]]`

Specify unix owner of chrony keys file, defaults to 0.

Default value: `0`

##### <a name="-chrony--config_keys_group"></a>`config_keys_group`

Data type: `Variant[Integer[0],String[1]]`

Specify unix group of chrony keys files, defaults to 0 on ArchLinux and chrony on Redhat.

Default value: `0`

##### <a name="-chrony--config_keys_mode"></a>`config_keys_mode`

Data type: `Stdlib::Filemode`

Specify unix mode of chrony keys files, defaults to 0644 on ArchLinux and 0640 on Redhat.

Default value: `'0640'`

##### <a name="-chrony--keys"></a>`keys`

Data type: `Array[String[1]]`

An array of key lines.  These are printed as-is into the chrony key file.

Default value: `[]`

##### <a name="-chrony--driftfile"></a>`driftfile`

Data type: `Stdlib::Unixpath`

A file for chrony to record clock drift in.

Default value: `'/var/lib/chrony/drift'`

##### <a name="-chrony--local_stratum"></a>`local_stratum`

Data type: `Variant[Boolean[false],Integer[1,15]]`

Override the stratum of the server which will be reported to clients
when the local reference is active. Use `false` to not set local_stratum in
chrony configuration.

Default value: `10`

##### <a name="-chrony--local_orphan"></a>`local_orphan`

Data type: `Boolean`

Put the server in 'orphan' mode when the local reference is active. Does
nothing if local_stratum is not set.

Default value: `false`

##### <a name="-chrony--ntpsigndsocket"></a>`ntpsigndsocket`

Data type: `Optional[Stdlib::Unixpath]`

This sets the location of the Samba ntp_signd socket when it is running as a Domain Controller (DC).

Default value: `undef`

##### <a name="-chrony--stratumweight"></a>`stratumweight`

Data type: `Optional[Numeric]`

Sets how much distance should be added per stratum to the synchronisation distance when chronyd
selects the synchronisation source from available sources.
When not set, chronyd's default will be used, which since version 2.0 of chrony, is 0.001 seconds.

Default value: `undef`

##### <a name="-chrony--log_options"></a>`log_options`

Data type: `Optional[String[1]]`

Specify which information is to be logged.

Default value: `undef`

##### <a name="-chrony--logbanner"></a>`logbanner`

Data type: `Optional[Integer[0]]`

Specify how often the log banner is placed in the logfile.

Default value: `undef`

##### <a name="-chrony--logchange"></a>`logchange`

Data type: `Float`

Sets the threshold for the adjustment of the system clock that will generate a syslog message.
Clock errors detected via NTP packets, reference clocks, or timestamps entered via the settime
command of chronyc are logged.

Default value: `0.5`

##### <a name="-chrony--package_ensure"></a>`package_ensure`

Data type: `String[1]`

This can be set to 'present' or 'latest' or a specific version to choose the
chrony package to be installed.

Default value: `'present'`

##### <a name="-chrony--package_name"></a>`package_name`

Data type: `String[1]`

This determines the name of the package to install.

Default value: `'chrony'`

##### <a name="-chrony--package_source"></a>`package_source`

Data type: `Optional[String]`

Source for the package when not wanting to install from a package repository.  This is required if
[`package_provider`](#package_provider) is set to `rpm` or `dpkg`.

Default value: `undef`

##### <a name="-chrony--package_provider"></a>`package_provider`

Data type: `Optional[String]`

Override the default package provider with a specific backend to use when installing the chrony package.
Also see [`package_source`](#package_source).

Default value: `undef`

##### <a name="-chrony--peers"></a>`peers`

Data type: `Chrony::Servers`

This selects the servers to use for NTP peers (symmetric association).
It can be an array of peers or a hash of peers with their respective options.

Default value: `[]`

##### <a name="-chrony--servers"></a>`servers`

Data type: `Chrony::Servers`

This selects the servers to use for NTP servers.  It can be an array of servers
or a hash of servers to their respective options. If an array is used, `iburst` will be configured for each server.
If you don't want to use `iburst`, use a hash instead.

Default value:

```puppet
{
    '0.pool.ntp.org' => ['iburst'],
    '1.pool.ntp.org' => ['iburst'],
    '2.pool.ntp.org' => ['iburst'],
    '3.pool.ntp.org' => ['iburst'],
  }
```

##### <a name="-chrony--pools"></a>`pools`

Data type: `Chrony::Servers`

This is used to specify one or more *pools* of NTP servers to use instead of individual NTP servers.
Similar to [`server`](#server), it can be an array of pools, (using iburst), or a hash of pools to their respective options.
See [pool](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#pool)

Default value: `{}`

##### <a name="-chrony--minsources"></a>`minsources`

Data type: `Optional[Integer[1]]`

Sets the minimum number of sources that need to be considered as selectable in the source selection algorithm
before the local clock is updated.

Default value: `undef`

##### <a name="-chrony--minsamples"></a>`minsamples`

Data type: `Optional[Integer[1]]`

Specifies the minimum number of readings kept for tracking of the NIC clock.

Default value: `undef`

##### <a name="-chrony--refclocks"></a>`refclocks`

Data type: `Array`

List of `refclock` directives to be added to the chrony configuration file.
Each element of the list should be a string which completes the `refclock` `chrony.conf` directive.

Example:
```puppet
refclocks => [
  'PPS /dev/pps0 lock NMEA refid GPS',
  'SHM 0 offset 0.5 delay 0.2 refid NMEA noselect',
  'PPS /dev/pps1:clear refid GPS2',
],
```

Default value: `[]`

##### <a name="-chrony--makestep_seconds"></a>`makestep_seconds`

Data type: `Numeric`

Configures the [`makestep`](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#makestep) `threshold`.
Normally chronyd will cause the system to gradually correct any time offset, by slowing down or speeding up the clock as required.
If the adjustment is larger than `makestep_seconds`, chronyd will step the clock.
Also see [`makestep_updates`](#makestep_updates).

Default value: `10`

##### <a name="-chrony--makestep_updates"></a>`makestep_updates`

Data type: `Integer`

Configures the [`makestep`](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#makestep) `limit`.
Chronyd will step the time only if there have been no more than `makestep_updates` clock updates.
Set to a negative value to disable the limit (useful for virtual machines and laptops that may get suspended for a prolonged time).
Also see [`makestep_seconds`](#makestep_seconds).

Default value: `3`

##### <a name="-chrony--queryhosts"></a>`queryhosts`

Data type: `Array[String[0]]`

This adds the networks, hosts that are allowed to query the daemon.

Default value: `[]`

##### <a name="-chrony--denyqueryhosts"></a>`denyqueryhosts`

Data type: `Array[String[0]]`

Similar to queryhosts, except that it denies NTP client access to a particular subnet or host,
rather than allowing it.

Default value: `[]`

##### <a name="-chrony--port"></a>`port`

Data type: `Optional[Stdlib::Port]`

Port the service should listen on. Module default is `undef` which means that port
isn't added to chrony.conf, and chrony listens to the default ntp port 123 if
`queryhosts` is used.

Default value: `undef`

##### <a name="-chrony--service_enable"></a>`service_enable`

Data type: `Boolean`

This determines if the service should be enabled at boot.

Default value: `true`

##### <a name="-chrony--service_ensure"></a>`service_ensure`

Data type: `Stdlib::Ensure::Service`

This determines if the service should be running or not.

Default value: `'running'`

##### <a name="-chrony--service_manage"></a>`service_manage`

Data type: `Boolean`

This selects if puppet should manage the service in the first place.

Default value: `true`

##### <a name="-chrony--service_name"></a>`service_name`

Data type: `String[1]`

This selects the name of the chrony service for puppet to manage.

Default value: `'chronyd'`

##### <a name="-chrony--wait_enable"></a>`wait_enable`

Data type: `Boolean`

This determines if the chrony-wait service should be enabled at boot.

Default value: `false`

##### <a name="-chrony--wait_ensure"></a>`wait_ensure`

Data type: `Stdlib::Ensure::Service`

This determines if the chrony-wait service should be running or not.

Default value: `'stopped'`

##### <a name="-chrony--wait_manage"></a>`wait_manage`

Data type: `Boolean`

This selects if puppet should manage the chrony-wait service in the first place.

Default value: `false`

##### <a name="-chrony--wait_name"></a>`wait_name`

Data type: `String[1]`

This selects the name of the chrony-wait service for puppet to manage.

Default value: `'chrony-wait.service'`

##### <a name="-chrony--smoothtime"></a>`smoothtime`

Data type: `Optional[String]`

Specify the smoothing of the time parameter as a string, for example `smoothtime 50000 0.01`.

Default value: `undef`

##### <a name="-chrony--mailonchange"></a>`mailonchange`

Data type: `Optional[String[1]]`

Specify the mail you wanna alert when chronyd executes a sync grater than the `threshold`.

Default value: `undef`

##### <a name="-chrony--threshold"></a>`threshold`

Data type: `Float`

Specify the time limit for triggering events.

Default value: `0.5`

##### <a name="-chrony--lock_all"></a>`lock_all`

Data type: `Boolean`

Force chrony to only use RAM & prevent swapping.

Default value: `false`

##### <a name="-chrony--sched_priority"></a>`sched_priority`

Data type: `Optional[Integer[0,100]]`

Set the CPU thread scheduler, this value is OS specific.

Default value: `undef`

##### <a name="-chrony--leapsecmode"></a>`leapsecmode`

Data type: `Optional[Enum['system', 'step', 'slew', 'ignore']]`

Configures how to insert the leap second mode.

Default value: `undef`

##### <a name="-chrony--leapsectz"></a>`leapsectz`

Data type: `Optional[String]`

Specifies a timezone that chronyd can use to determine the offset between UTC and TAI.

Default value: `undef`

##### <a name="-chrony--maxdistance"></a>`maxdistance`

Data type: `Optional[Float]`

Sets the maximum root distance of a source to be acceptable for synchronisation of the clock.

Default value: `undef`

##### <a name="-chrony--maxslewrate"></a>`maxslewrate`

Data type: `Optional[Float]`

Maximum rate for chronyd to slew the time. Only float type values possible, for example: `maxslewrate 1000.0`.

Default value: `undef`

##### <a name="-chrony--ntsserverkey"></a>`ntsserverkey`

Data type: `Optional[Stdlib::Absolutepath]`

This directive specifies a file containing a private key in the PEM format for chronyd to operate as an NTS server.

Default value: `undef`

##### <a name="-chrony--ntsservercert"></a>`ntsservercert`

Data type: `Optional[Stdlib::Absolutepath]`

This directive specifies a file containing a certificate in the PEM format for chronyd to operate as an NTS server.

Default value: `undef`

##### <a name="-chrony--ntsport"></a>`ntsport`

Data type: `Optional[Stdlib::Port]`

This directive specifies the TCP port on which chronyd will provide the NTS Key Establishment (NTS-KE) service.

Default value: `undef`

##### <a name="-chrony--maxntsconnections"></a>`maxntsconnections`

Data type: `Optional[Integer[0]]`

This directive specifies the maximum number of concurrent NTS-KE connections per process that the NTS server will accept.

Default value: `undef`

##### <a name="-chrony--ntsprocesses"></a>`ntsprocesses`

Data type: `Optional[Integer[0]]`

This directive specifies how many helper processes will chronyd operating as an NTS server start for handling client NTS-KE requests in order to improve
        performance with multi-core CPUs and multithreading.

Default value: `undef`

##### <a name="-chrony--ntsdumpdir"></a>`ntsdumpdir`

Data type: `Optional[Stdlib::Absolutepath]`

This directive specifies a directory where chronyd operating as an NTS server can save the keys which encrypt NTS cookies provided to clients.

Default value: `undef`

##### <a name="-chrony--ntsntpserver"></a>`ntsntpserver`

Data type: `Optional[String]`

This directive specifies the hostname (as a fully qualified domain name) or address of the NTP server(s) which is provided in the NTS-KE response to the
        clients.

Default value: `undef`

##### <a name="-chrony--ntsrotate"></a>`ntsrotate`

Data type: `Optional[Integer[0]]`

This directive specifies the rotation interval (in seconds) of the server key which encrypts the NTS cookies.

Default value: `undef`

##### <a name="-chrony--clientlog"></a>`clientlog`

Data type: `Boolean`

Determines whether to log client accesses.

Default value: `false`

##### <a name="-chrony--clientloglimit"></a>`clientloglimit`

Data type: `Optional[Integer]`

When set, specifies the maximum amount of memory in bytes that chronyd is allowed to allocate for logging of client accesses.
If not set, chrony's, default will be used. In modern versions this is 524288 bytes.  Older versions defaulted to have no limit.
See [clientloglimit](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#clientloglimit)

Default value: `undef`

##### <a name="-chrony--rtcsync"></a>`rtcsync`

Data type: `Boolean`

Sync system clock to RTC periodically

Default value: `true`

##### <a name="-chrony--rtconutc"></a>`rtconutc`

Data type: `Boolean`

Keep RTC in UTC instead of local time.
If not set, chrony's, default will be used. On Arch Linux the default is true instead.
See [rtconutc](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html#rtconutc)

Default value: `false`

##### <a name="-chrony--hwtimestamps"></a>`hwtimestamps`

Data type: `Variant[Hash,Array[String]]`

This selects interfaces to enable hardware timestamps on. It can be an array of
interfaces or a hash of interfaces to their respective options.

Default value: `[]`

##### <a name="-chrony--dumpdir"></a>`dumpdir`

Data type: `Optional[Stdlib::Unixpath]`

Directory to store measurement history in on exit.

Default value: `undef`

##### <a name="-chrony--maxupdateskew"></a>`maxupdateskew`

Data type: `Optional[Float]`

Sets the threshold for determining whether an estimate might be so unreliable that it should not be used

Default value: `undef`

##### <a name="-chrony--acquisitionport"></a>`acquisitionport`

Data type: `Optional[Integer[1,65535]]`

Sets the acquisitionport for client queries

Default value: `undef`

## Data types

### <a name="Chrony--Servers"></a>`Chrony::Servers`

This type is for the `servers`, `pools` and `peers` parameters.

#### Examples

##### A hash of servers

```puppet
{
  'ntp1.example.com => [
    'minpoll 3',
    'maxpoll 6',
  ],
  'ntp2.example.com => [
    'iburst',
    'minpoll 4',
    'maxpoll 8',
  ],
}
```

##### An array of servers

```puppet
[
  'ntp1.example.com',
  'ntp2.example.com',
]
```

Alias of `Variant[Hash[Stdlib::Host, Optional[Array[String]]], Array[Stdlib::Host]]`

