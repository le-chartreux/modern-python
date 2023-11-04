# [Modern Python](https://github.com/le-chartreux/modern-python/)

*Modern Python* is an educational resource that covers key aspects of writing high-quality modern Python programs and the tools available to ensure their quality.
The aim of *Modern Python* is to provide to the reader a methodology for carrying out Python projects in a modern way, with a small set of reliable and sustainable tools, in order to simplify their development.
While it does not delve into [programming principles that apply to every modern language](https://en.wikipedia.org/wiki/Category:Programming_principles) (for which you can refer to the excellent book [Clean Code](https://www.pearson.com/en-us/subject-catalog/p/clean-code-a-handbook-of-agile-software-craftsmanship/P200000009044?view=educator), by Robert C. Martin) it focuses on Python-specific rules.
By following this documentation, you can ensure that your Python programs are not only functional but also maintainable and easy to understand.

## Introduction

Software development work is constantly evolving.
The days when a software was created, tested, put into production and never changed are long gone (if they ever existed).
New needs arise regularly, whether functional or not: adding functionalities, installing on new types of ma-
chines, adapting to new standards...
Meeting all these needs requires ever more modifications to the original code, grouped together under the general term «maintenance».
To manage the organization of maintenance, agile methods have replaced the old development methods.
However, it is still necessary to work with old code and to produce new code.
In a world where software maintenance is becoming an increasingly important part of the IT department’s workload, the project management method must not remain the only agile element in a team: it has become a necessity to produce software that are *agile*.
Software that are easy for end-users to install.
Software for which it is possible to modify the code without undermining its foundations.
Software that can be easily understood by a collaborator taking over from us.
Not just functional software.
Software that are *clean*.

*Modern Python* is largely inspired by the article [Hypermodern Python](https://cjolowicz.github.io/posts/hypermodern-python-01-setup/), written by Claudio Jolowicz.
*Hypermodern Python* is a comprehensive tutorial details the main domains of Python software quality through six chapters: [Setup](https://cjolowicz.github.io/posts/hypermodern-python-01-setup/), [Testing](https://cjolowicz.github.io/posts/hypermodern-python-02-testing/), [Linting](https://cjolowicz.github.io/posts/hypermodern-python-03-linting/), [Typing](https://cjolowicz.github.io/posts/hypermodern-python-04-typing/), [Documentation](https://cjolowicz.github.io/posts/hypermodern-python-05-documentation/) and [CI/CD](https://cjolowicz.github.io/posts/hypermodern-python-06-ci-cd/).
However, although very interesting, this tutorial has several peculiarities which make it unsuitable for practical application in its current state for a company:

- Too many tools are presented, with some encroaching on the use cases of others.
- No updates since 2020, so some parts are obsolete.
- A tendency to present overly cutting-edge technologies, which have since been abandoned by their creators, or are likely to be in the near future.
- Time-consuming, as it took me over a week to follow it in its entirety.

As a result, I’ve undertaken to write an article reviewing the aspects of *Hypermodern Python*, while correcting these points.

## Getting started

You can either follow the [tutorial](tutorial/README.md) to learn by doing, or the [guide](guide/README.md) to learn by theory.
Both approaches are complementary and can help you gain a deeper understanding of the subject.
