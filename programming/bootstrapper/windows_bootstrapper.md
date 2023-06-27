# Windows Bootstrapper

The goal here is to automate the installation of dependencies. The basics here is that it is installed through a set of XML manifests that specifies the metadata to manage the installation of components. It will also describe how the dependencies should be installed.

## Creating a Custom Bootstrapper Package

You can generate a bootstrapper manifest by using the XML editor in Visual Studio. You will need the a product manifest and maybe a package manifest as well.
- For the product manifest, you will need the `product.xml` containing language neutral metadata. Metadata common to all the localized versions of the redistribution component. To create this file, you can look at the online resource.
- The package manifest requires the `package.xml` file that contains language specific metadata; it will also contain localized error messages. A component must have at least one package manifest for each localized version of that component. There is also online resource on how this is done.

## Pointers

| Name + Link                                                    | Description                                                                     |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| [Custom Bootstrapper Tutorial](windows_custom_bootstrapper.md) | This page contains notes on how to get custom bootstrappers working on windows. |
|                                                                |                                                                                 |
