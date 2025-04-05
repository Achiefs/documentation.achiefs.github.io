---
layout: default
title: Configuration file
nav_order: 3
---

# Configuration file
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# Configure File Integrity Monitor

If you want to customize your installation and monitor custom folders in addition to the given ones. It is required to edit the `config.yml` file located at `C:\Program Files\File Integrity Monitor\config.yml` (Windows systems) or `/etc/fim/config.yml` (Unix systems).

In the following sections, you could review each section and parameters to tune up your configuration as you require.

{: .note }
> <div markdown="block">
> Advanced
> {: .label .label-red }
> </div>
> The tag `Advanced` mentions parameters that could affect the FIM function, and it could break something. Be sure before changing some of these options.

    

---

# Parameters
## node

String
{: .label }

Default value: `FIM`.

Define the event producer's name.

This parameter will come on each event produced by the process.

---

- ## events

    Section
    {: .label .label-green }

    Handle event output parameters.

    - ### watcher

    String
    {: .label }

    Default value: `Recommended`.

    Select the watcher type used to detect the events. Recommended will use the suggested watcher for each system. The poll option will use polling to get event changes (Recommended for Fargate/ECS/EKS environments).
    
    The supported options are [Recommended, Poll].

    - ### destination

    String
    {: .label }

    Default value: `file`.

    It defines the destination of the events.
    
    The supported options are [file, network, both].

    - ### file

    String
    {: .label }

    Default value: `C:\ProgramData\fim\events.json` for Windows systems, `/var/lib/fim/events.json` for Unix systems.

    Defines where the events will be stored.

    It receives a system path, ex: `C:\Users\events.json` (Windows systems) or `\home\events.json` (Unix systems).

    - ### max_file_checksum 

    Integer
    {: .label .label-purple }
    Advanced
    {: .label .label-red }

    Default value: `64`.

    Defines the maximum size of the file to get its hash (checksum) in megabytes.

    To speed up hashing, decrease this value, minimum value `1`, and maximum value `128`, more than that will increase the event processing time and CPU consumption.

    - ### max_file_size

    Integer
    {: .label .label-purple }
    Advanced
    {: .label .label-red }

    Default value: `128`.

    Defines the maximum size of `events.json` file before being rotated.

    we recommend to maintain this value as default. Increasing it will allow to rotate the file less times. Decreasing it will increase the rotations of the file.

    - ### endpoint

        Section
        {: .label .label-green }

        Handle network parameters. 

        - #### address

        String
        {: .label }

        Default value: `None`.

        It defines the IP/DNS of indexer software currently supported by indexers ElasticSearch, OpenSearch and Wazuh-indexer.

        Format example: `0.0.0.0` for IP, `indexer.example.com` for DNS.

        - #### insecure

        Boolean
        {: .label .label-purple }

        Default value: `false`.

        It defines the trust of HTTPS certificates of the indexer endpoint.

        - #### credentials

            Section
            {: .label .label-green }

            Handle endpoint access credentials.
            For ElasticSearch/OpenSearch FIM requires `user` and `password` parameters.
            For Splunk FIM requires only `token` parameter.

            - ##### user

            String
            {: .label }

            Default value: `None`.

            Defines the username credential to push events into the indexer endpoint.

            - ##### password

            String
            {: .label }

            Default value: `None`.

            Defines the password credential to push events into the indexer endpoint.

            - ##### token

            String
            {: .label }

            Default value: `None`.

            Store the Splunk HTTP event collector token to push events to Splunk indexer endpoint.

---

- ## audit

    Section
    {: .label .label-green }

    Keeps a list of files or directories to monitor. This section will use the Audit daemon engine with enhanced information.
    
    Include as many elements as you require.

    - ### path

        String
        {: .label }

        It defines the directory or files to monitor. It applies recursion.

        - #### ignore

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Allows to ignore files that match the given string inside its name.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### allowed

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Set the allowed strings to trigger events, events in this path will trigger if the file contains any of configured strings.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### exclude

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Set the excluded folders inside the Audit path given. Set a path outside of the Audit parent path will produce unexpected behaviour.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### labels

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Allows to define custom labels on each event produced at the given path.

        - #### rule

        String
        {: .label}

        Default value: `wax`.

        Allows to define custom Audit rule at the given path.

{: .note }
> The `rule` parameter support the following characters in any order:
> - `r` or `R`, enable read events at the given path.
> - `w` or `W`, enable write events at the given path.
> - `a` or `A`, enable attributes change events at the given path.
> - `x` or `X`, enable execution of code events at the given path.
> 
> Examples of the format:
> - `rwax`, to detect all kind of events (It could be noisy).
> - `wax`, default value to detect write, attribute change and execution.
> - `w`, value to detect directory write changes.

---

- ## monitor

    Section
    {: .label .label-green }

    Keeps a list of files or directories to monitor.
    
    Include as many elements as you require.

    - ### path

        String
        {: .label }

        It defines the directory or files to monitor. It applies recursion.

        - #### ignore

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Allows to ignore files that match the given string inside its name.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### allowed

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Set the allowed strings to trigger events, events in this path will trigger if the file contains any of configured strings.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### exclude

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Set the excluded folders inside the Monitor path given. Set a path outside of the Monitor parent path will produce unexpected behaviour.
        
        Available formats Array or List. Consult the note at the end of the section.

        - #### labels

        Array
        {: .label .label-yellow }
        String
        {: .label}

        Allows to define custom labels on each event produced at the given path.

---

- ## hashscanner

    Section
    {: .label .label-green }

    Defines the current behaviour of file hash scans.

    Hash scanner will take your primary engine config paths to be scanned.
    If you only have Audit paths defined Hash scanner will scan over those paths.
    If you only have Monitor paths defined Hash scanner will scan monitor section defined paths.
    If both engines are defined Hash scanner will select Audit (as usually is the critical one).


    - ### file

    String
    {: .label }

    Default value: `C:\ProgramData\fim\fim.db` for Windows systems, `/var/lib/fim/fim.db` for Unix systems.

    Defines where the hash database will be stored.

    It receives a system path, ex: `C:\Users\events.json` (Windows systems) or `\home\events.json` (Unix systems).

    - ### enabled

    Boolean
    {: .label .label-purple }

    Default value: `true`.

    It defines whether the hash scanner thread starts or not.

    - ### interval

    Integer
    {: .label .label-purple }
    Advanced
    {: .label .label-red }

    Default value: `60`.

    Defines the window interval to run hash scans, hashscanner thread will sleep the defined interval.

    To speed up scans, decrease this value, minimum value `5` (not recommended for bigger paths more than 5.000 files), and suggested as maximum value `1440` (24h), more than that will introduce security risks. This scan is not intended for real-time analysis for that matter you should use Monitor or Audit engine.

    - ### algorithm

    String
    {: .label}

    Default value: `Sha256`.

    Allows to define hashing algoritmh applied to each file.

{: .note }
> The `algorithm` parameter support the following values:
> - `Sha224` or `sha224` or `SHA224` or `224`, use Sha224 as hashing algorithm.
> - `Sha256` or `sha256` or `SHA256` or `256`, use Sha256 as hashing algorithm.
> - `Sha384` or `sha384` or `SHA384` or `384`, use Sha384 as hashing algorithm.
> - `Sha512` or `sha512` or `SHA512` or `512`, use Sha512 as hashing algorithm.
> - `Keccak224` or `keccak224` or `KECCAK224` or `K224`, use Keccak224 as hashing algorithm.
> - `Keccak256` or `keccak256` or `KECCAK256` or `K256`, use Keccak256 as hashing algorithm.
> - `Keccak384` or `keccak384` or `KECCAK384` or `K384`, use Keccak384 as hashing algorithm.
> - `Keccak512` or `keccak512` or `KECCAK512` or `K512`, use Keccak512 as hashing algorithm.
>
> If `algorithm` is changed after FIM first scan (`fim.db` file is present) you should remove `fim.db` file to avoid false positive events.
>
> Take into account that increasing the hash algorithm could lead to higher scan times so keep in mind the relation between interval and algorithm.

---

- ## log

    Section
    {: .label .label-green }

    It Keeps the configuration of logging output.

    - ### file

    String
    {: .label }

    Default value: `C:\ProgramData\fim\fim.log` for Windows systems, `/var/log/fim/fim.log` for Unix systems.

    Defines where the logs are stored.

    - ### level

    String
    {: .label }

    Default value `info`.

    Defines the level of verbosity logged to the log file.
    
    The supported options are [debug, info, error and warning].

    - ### max_file_size

    Integer
    {: .label .label-purple }
    Advanced
    {: .label .label-red }

    Default value: `64`.

    Defines the maximum size of `fim.log` file before being rotated.

    we recommend to maintain this value as default. Increasing it will allow to rotate the file less times. Decreasing it will increase the rotations of the file.

{: .note }
> The `ignore`,`allowed` and `exclude` parameters has two different formats:
> ```
>   - path: /tmp/dir
>     ignore: [.txt, .tmp]
> ```
> Or list variant: 
> ```
>   - path: /tmp/dir
>     ignore:
>       - .txt
>       - .tmp
> ```

{: .note }
> The `labels` parameter has two different formats:
> ```
>   - path: /tmp/dir
>     labels: ["temp", "linux"]
> ```
> Or list variant:
> ```
>   - path: /tmp/dir
>     labels:
>       - temp
>       - linux
> ```

---

## Example configuration

FIM comes with a ready-to-use configuration. You can tune up as you wish. Here you can see an example configuration:

Windows systems:
```
node: "FIM"

# Events configuration, where to store produced events
events:
  watcher: Recommended
  destination: both
  file: C:\ProgramData\fim\events.json
  max_file_checksum: 64
  endpoint:
    address: "https://127.0.0.1:9200"
    insecure: true
    credentials:
      user: "admin"
      password: "admin"

# Monitor folder or files.
monitor:
  - path: C:\Program Files\
    labels: ["Program Files", "windows"]
  - path: C:\Users\
    labels: ["Users", "windows"]
    allowed: [".txt", ".doc"] 
    exclude: 
      - C:\Users\Temp

# App procedure and errors logging
log:
  file: C:\ProgramData\fim\fim.log
  # Available levels [debug, info, error, warning]
  level: info
```

Linux systems:
```
node: "FIM"

# Events configuration, where to store produced events
events:
  watcher: Recommended
  destination: both
  file: /var/lib/fim/events.json
  max_file_checksum: 64
  endpoint:
    address: "https://127.0.0.1:9200"
    insecure: true
    credentials:
      user: "admin"
      password: "admin"

# Audit extended files and folders information
audit:
  - path: /tmp
    labels: ["tmp", "linux"]
    ignore: [".swp"]
    allowed: [ ".txt", ".odt" ]

# Simple files and folders information
monitor:
  - path: /bin/
  - path: /usr/bin/
    labels: ["usr/bin", "linux"]
  - path: /etc
    labels: ["etc", "linux"]
    exclude: [ "/etc/libvirt/qemu" ]

# App procedure and errors logging
log:
  file: /var/log/fim/fim.log
  # Available levels [debug, info, error, warning]
  level: info
```

macOS systems:
```
node: "FIM"

# Events configuration, where to store produced events
events:
  watcher: Recommended
  destination: both
  file: /var/lib/fim/events.json
  max_file_checksum: 64
  endpoint:
    address: "https://127.0.0.1:9200"
    insecure: true
    credentials:
      user: "admin"
      password: "admin"

# Monitor files and folders.
monitor:
  - path: /tmp/
  - path: /bin/
  - path: /usr/bin/
    labels: ["usr/bin", "macos"]
  - path: /etc
    labels: ["etc", "macos"]

# App procedure and errors logging
log:
  file: /var/log/fim/fim.log
  # Available levels [debug, info, error, warning]
  level: info
```
