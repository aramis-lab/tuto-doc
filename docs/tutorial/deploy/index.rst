Deploy your documentation
=========================

To conclude this tutorial, now that our documentation is ready
to be shared publicly, we will **deploy** our documentation
on the internet.

To do this, we will try two tools: `GitHub Pages <https://docs.github.com/en/pages/quickstart>`_ and
`Read the Docs <https://about.readthedocs.com/>`_, starting with the simplest one, GitHub Pages.

.. important::
   In these sections, we will do as if we had merged the changes made on the branch ``tutorial`` in our
   ``main`` branch, and skip the merge that can be fastidious due to conflicts. So, commit your changes on ``tutorial``,
   publish your branch with ``git push --set-upstream origin tutorial``, and checkout to the ``main`` branch.

   Don't be surprised if you see new sections when your documentation is deployed. This is because ``main`` contains
   additional pages.

.. toctree::
   :maxdepth: 1
   
   github_pages
   read_the_docs