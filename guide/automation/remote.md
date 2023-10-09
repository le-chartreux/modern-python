# Remote

Running automation on a CI/CD server has several advantages.
For one, it allows you to run actions across different operating systems and on fresh installations, making your workflows platform-independent.
Additionally, CI/CD servers allow you to run actions in response to an event at any time, making it easy to automate your workflows and ensure that your code is always up-to-date.
By leveraging the power of a CI/CD server, you can easily scale your workflows, collaborate with team members, and implement continuous integration and deployment, all while ensuring consistency and reproducibility.

If you use [Git](https://git-scm.com/) (which you should!) with [GitHub](https://github.com/), you have access to a very easy-to-use CI/CD system called [GitHub Actions](https://docs.github.com/en/actions).
With [GitHub Actions](https://docs.github.com/en/actions), you can easily automate your workflows to test, assert quality, and deploy your code directly from your [GitHub](https://github.com/) repository.

While explaining how to set up a full CI/CD environment is beyond the scope of this tutorial, there are many resources available to help you get started.
In general, you will need to define a series of workflows that automate your build, test, quality checks, and deployment processes.

For Python software quality, I recommend setting up these two actions:

- Running [Tox](local.md) on each commit to ensure the quality of your software.
- [Deploying](../project/deployment.md) your software on each release, after ensuring that [Tox](local.md) hasn't detected any issues.

By implementing these actions, you can ensure that your code is always of high quality and that your deployments are consistent and reliable.
