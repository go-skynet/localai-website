
+++
disableToc = false
title = "Easy Setup Demo"
weight = 2
+++

This is for `Linux`, `Mac OS`, or `Windows` Hosts.

The goal of this how to is to get you setup with a demo fast.

This demo is going to act like you have nothing already installed, if you already have docker or other tools installed feel free to skip the step listed.

Download these --> [Docker Desktop](https://docs.docker.com/engine/install/), [Python 3.11](https://www.python.org/downloads/release/python-3110/), [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

Install `docker`, `python3.11`, and `git`... Cool! (Skip this if you already have them installed)

Make a folder named `LocalAi` then run `git clone https://github.com/lunamidori5/localai-lunademo.git`

Move into the folder that github made `localai-lunademo`.

Run `Setup.sh` (Linux or Mac) or `Setup.bat` (Windows), this will setup everything for you.

The setup file will start up a python env - you will see the folder be made. It will then auto install all of the pip installs it needs to work inside of the python env. Then it will run the main.py, you can also bypass what ever steps you want or use the code how you want, but if you change the code and need support please let the support person know.

Enjoy localai! (If you need help contact Luna Midori on Discord)

{{% notice Issues %}}
- `Git Bash` on Windows is not working.
- Running over `SSH` or other remote cmd may bug out, load slowly, or crash.
{{% /notice %}}
