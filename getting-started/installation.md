# Installation

Install Orchestralib Python library by running

```
pip install orchestralib \
--trusted-host=olib-packages.s3-website-us-west-1.amazonaws.com  \
--extra-index-url=http://olib-packages.s3-website-us-west-1.amazonaws.com
```

If reinstalling, run the same command as above, but include the additional parameter&#x20;

`--upgrade`

{% hint style="info" %}
Orchestralib works on MacOS and Linux.&#x20;

Depending on the version of Python 3 you're using, and how it was installed, you may need to call `pip3` instead of `pip`.

For any python-related issues:

* try installing Python3 using homebrew i.e.) \
  `brew install python`

For installation-related issues:

* ensure you're using the latest version of pip (or pip3) by running \
  `pip install --upgrade pip`
* ensure you are using the latest version of setuptools by running \
  `python3 -m pip install --upgrade setuptools`
{% endhint %}

**Coming soon:** `pip install orchestralib` directly from PyPi.
