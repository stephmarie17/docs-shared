=============
Issues & Help
=============

We are lucky to have a vibrant developer community that includes users that
have various levels of experience using the {+driver-short+}. The quickest way
to get support for general questions is through the `MongoDB Community Forums <https://www.mongodb.com/community/forums/>`__.

To learn more about our support channels, see :manual:`</support/>` in the
MongoDB Server documentation.

Bugs / Feature Requests
-----------------------

To report a bug or request a new feature in the {+driver-short+}, open
a case in the issue management tool, JIRA, by performing the following steps:

1. Visit the `MongoDB JIRA issue tracker <https://jira.mongodb.org/>`__ and
   `register or login <https://account.mongodb.com/account/register>`__.
   Then, log in to JIRA.
#. Navigate to the |JIRA-project-target|.
#. Click :guilabel:`Create` to create a ticket. Please provide as much
   information as possible about the issue or request in the ticket.

.. note::

   Bug reports in the |JIRA-project-code| JIRA project are publicly viewable.

If you identify a security vulnerability in any official MongoDB product,
please report it according to the instructions found in the
:manual:`Create a Vulnerability Report </tutorial/create-a-vulnerability-report>`
page in the MongoDB Server documentation.

Pull Requests
-------------

We welcome contributions to improve the {+driver-short+}. We guide user
contributions to ensure they meet the codebase standards. Please ensure that
your pull request includes documentation, tests, and pass the integration and
unit tests in the source code repository.

To get started, clone the {+driver-short+} repository and create a feature
branch by running the following shell commands:

.. code-block:: bash

   $ git clone {+driver-repo-gitfile+}
   $ cd {+driver-repo-path+}
   $ git checkout -b myNewFeature

After making any code changes, follow the |test-guideline-target| to ensure
your code passes any newly added and existing tests. Then, push your changes
to your branch and open a pull request in the |driver-repo-target| on GitHub.
