Read the Docs
=============

Let's get straight to the point. To deploy your documentation with `Read the Docs <https://about.readthedocs.com/>`_:

1. Create a ``.readthedocs.yaml`` at the root of your project on the ``main`` branch (no need to
   do it here, there is already one). This file will tell Read the Docs what to do to build the
   documentation.

.. dropdown:: ``.readthedocs.yaml``

    .. code-block:: yaml

        # Read the Docs configuration file
        # See https://docs.readthedocs.io/en/stable/config-file/v2.html for details

        # Required
        version: 2

        # Set the OS, Python version, and other tools you might need
        build:
            os: ubuntu-24.04
            tools:
                python: "3.12"
            jobs:
                post_create_environment:
                    - pip install poetry
                    - poetry config virtualenvs.create false
                    - . "$READTHEDOCS_VIRTUALENV_PATH/bin/activate" && poetry install --with docs

        # Build documentation in the "docs/" directory with Sphinx
        sphinx:
            configuration: docs/conf.py

2. Got to https://about.readthedocs.com/.
3. Log in with your GitHub account: **Log In > Read the Docs Community > Log in using GitHub**.
4. Click on **Add project**, and fill the fields with:
    - *Repository name*: select ``<github-username>/tuto-doc``
    - *Name*: ``NeuroPlot-<github-username>``
    - *Default branch*: ``main``

And, here we go! Let's just wait a few minutes that Read the Docs deploy the website, which will be accessible at:
``https://neuroplot-{github-username}.readthedocs.io/``.

Once on your website, on the bottom right, click on the green button **latest**. These are the
available versions of our documentation. Currently, the only version available is *latest*, which is the latest
version on our default branch (``main`` here).

Versioning
----------

To test Read the Docs versioning functionalities, we will create different versions of our project on the
``main`` branch:

.. code-block:: bash

    echo "\nVersion 0.1.0" >> index.rst
    git add .
    git commit -m "version 0.1.0"
    git tag v0.1.0
    ed -s index.rst <<< $'$d\n$a\nVersion 0.2.0\n.\nwq'
    git add .
    git commit -m "version 0.2.0"
    git tag v0.2.0
    ed -s index.rst <<< $'$d\n$a\nVersion latest\n.\nwq'
    git add .
    git commit -m "Latest version"
    git push
    git push --tags

Don't worry about these commands, they just add three dummy commits that will simulate
three different versions of our projects. The first commit is tagged "v0.1.0", and the
second is tagged "v0.2.0". The last one doesn't have tag, it represents the latest version of our projects that
is not stable yet.

Now, we would like to see all these versions in our public documentation.

If you come back to the Read the Docs dashboard, you will see that a new version of your project appeared: *stable*,
which corresponds to the documentation build from your **latest tagged version** (``v0.2.0`` here).

Then, in the Read the Docs dashboard, go to **Settings > Default version** and choose "stable".

And, once the deployment is finished, if you go to your documentation website (``https://neuroplot-{github-username}.readthedocs.io/``),
you can see that you have now two versions available on the bottom right: *stable* and *latest*. By default, we now
land on the *stable* version.

Finally, to add other versions:

1. In the Read the Docs dashboard, click on **Add version**.
2. Select the versions you want to deploy. A version can be either a tag or a branch, but make
   sur that this tag or branch have a ``.readthedocs.yaml``. Here we will select the tag ``v0.1.0`` and the branch ``doc``.
3. Check the box **Active**.
4. Click on **Update version**.

Once again, give Read the Docs time to build these versions, and go to your online documentation to see the result!

.. note::
    With Read the Docs, changes can take some time to appear on your documentation. Be patient!
    Cleaning your browser's cache and history can help!