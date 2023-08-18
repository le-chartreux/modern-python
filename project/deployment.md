# Deployment

Deployment is a crucial aspect of any project, as it determines how easily users can install and use your tool.
If the installation process is complicated, users may have a bad first impression or may not use it at all.
There are various approaches to deploying on different platforms, but the ultimate goal is always the same: to make it easy for the end-user to install your product with just one or two commands.

If your project is open source and you want to deploy it on [PyPI](https://pypi.org/) (the main Python package index), you can refer to the official Python documentation's [packaging projects tutorial](https://packaging.python.org/en/latest/tutorials/packaging-projects/).
This tutorial is well-made and maintained, so it's recommended to follow it.

For other cases, you can refer to the package index you're using.
If you're using a self-hosted index, you can check the Python documentation on [hosting your own index](https://packaging.python.org/en/latest/guides/hosting-your-own-index/).
For general-purpose indexes like [JFrog Artifactory](https://jfrog.com/artifactory/), [Azure Artifact](https://azure.microsoft.com/en-in/products/devops/artifacts), and [Sonatype Nexus](https://www.sonatype.com/products/sonatype-nexus-repository), look at their specific documentation on Python packaging.
