
+++
disableToc = false
title = "Easy Setup Demo"
weight = 2
+++

This is for `Linux` or `Windows` Hosts only. Sorry Mac friends (Contact Luna on discord if you have a mac and want to help with this page)
The goal of this how to is to get you setup with a demo fast.

This demo is going to act like you have nothing already installed, if you already have docker or other tools installed feel free to skip the step listed.

Download these --> [Docker Desktop](https://docs.docker.com/engine/install/), [Demo Rar File](https://drive.google.com/file/d/1p2_-WdS15aVvR8yoJixvlg1t9nHgAhqQ/view?usp=sharing), [Demo Model](https://huggingface.co/TheBloke/WizardLM-13B-V1.2-GGML/resolve/main/wizardlm-13b-v1.2.ggmlv3.q4_0.bin)

Install docker... Cool!

Unrar the demo rar file into a folder called `LocalAi`

Open a CMD or Bash window. 

Type in `docker-compose up --pull always` -> This installs a LocalAi docker

Move the Wizard model into the models folder. Do not rename it.

Once localai is done setting up, in a new CMD or Bash window.

type `python main.py` and enjoy your localai setup
