Example Manifest
---------------------

Although we can deploy apps without a manifest, manifests provide consistency and 
reproducibility. This can be useful when you want your apps to be portable between
different clouds.

Manifests are written in YAML. The manifest below illustrates some YAML conventions, 
as follows:

    The manifest begins with three dashes.
    The applications block begins with a heading followed by a colon.
    The application name is preceded by a single dash and one space.
    Subsequent lines in the block are indented two spaces to align with name.

---
applications:
- name: my-app
  memory: 512M
  instances: 2
  buildpack: java_buildpack  (or buildpack url)
  no-route: true
  random-route: true
  routes:
  - route: example.com
  - route: www.example.com/foo
  - route: tcp-example.com:1234
  env:
    RAILS_ENV: production
    RACK_ENV: production
  services:
  - instance_ABC
  - instance_XYZ



A minimal manifest requires only an application name.


How cf push Finds the Application
--------------------------------------

By default, cf push recursively pushes the contents of the current working directory. 
Alternatively, you can provide a path using either a manifest or a command line option.

   > If the path is to a directory, cf push recursively pushes the contents of that directory 
       instead of the current working directory.
   > If the path is to a file, cf push pushes only that file.


Precedence Between Manifests, Command Line Options, and Most Recent Values
------------------------------------------------------------------------------------------

When you push an application for the first time, Cloud Foundry applies default values
to any attributes that you do not set in a manifest or cf push command line options.

> For example, cf push my-app with no manifest might deploy one instance of the app 
   with one gigabyte of memory. In this case the default values for instances and memory
   are “1” and “1G”, respectively.

> Between one push and another, attribute values can change in other ways.

    For example, the cf scale command changes the number of instances.

> cf push follows rules of precedence when setting attribute values:

    Manifests override most recent values, including defaults.
    Command line options override manifests.






