# Deployment

Deployment is a crutial part of any project: if installing your tool is complicated, your users will either don't use it or at least have a bad first impression about it.

It exists a lot of different approchs to deploy to a lot of different plateforms, so of course this tutorial can't conver them all.
Howevery, the ultimate goal is always the same: to give to the final user the possibility to install your product easily (and by easily I mean with only one or two commands).

If your project is open source and that you want it to be deployed on [PyPI](https://pypi.org/) (the main Python package index, where you connect when running [pip](https://pip.pypa.io/)), you can check the [packaging projects tutorial](https://packaging.python.org/en/latest/tutorials/packaging-projects/) on the official Python documentation website.
This tutorial clearly can't compare to the official documentation, that is really well-made and maintained, so please follow it.

For other case, refer to the package index you are using:

- For self-hosted indexes you can refer to the Python documentation about [hosting your own index](https://packaging.python.org/en/latest/guides/hosting-your-own-index/).
- For general purpose indexes like [JFrog Artifactory](https://jfrog.com/artifactory/), [Azure Artifact](https://azure.microsoft.com/en-in/products/devops/artifacts) and [Sonatype Nexus](https://www.sonatype.com/products/sonatype-nexus-repository), look at their specific documentation about Python packaging.
