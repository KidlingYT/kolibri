This is the documentation on setting up the Kolibri dev-server from Windows

1. Clone the fork.
```sh
   git clone https://github.com/KidlingYT/kolibri.git
```

Note: This will take some time, it's a big repo.

2. Make sure you have wsl enabled on your windows machine (`wsl --version` would confirm).

```sh
wsl
```

3. You should see some logs followed by a new terminal path at `mnt/...`

4. Install git large file storage:

```sh
cd kolibri
git lfs install
```

5. You should see
```
Updated Git hooks.
Git LFS initialized.
```

6. Update the git blame to handle large-scale commits

```sh
git config blame.ignoreRevsFile .git-blame-ignore-revs
```

7. Add the repo as upstream

```sh
 git remote add upstream git@github.com:learningequality/kolibri.git
```

8. Here is where things get tricky....

9. Set the clrf so that unix doesn't mess with script execution
```sh
git config --global core.autocrlf input
```

10. Clone the pyenv-virtualenv tool

```sh
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
```

11. Setup global execution

```sh
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

12. Restart

```sh
exec "$SHELL"
```

13. Create your python virtualenv

```sh
pyenv virtualenv 3.9.9 kolibri-py3.9
```
  python version ^^^^ name ^^^^

14. Activate the virtual environment

```sh
pyenv activate kolibri-py3.9
```

15. Set the dev environemnt up

```
# add this line at the end of your ~/.bash_profile file:
# Haha learn vim and deal with it

export KOLIBRI_RUN_MODE="dev"
```

16. Install packages (Make sure you are in your active venv!!)

P.S. this one is slow

```sh
pip install -r requirements.txt --upgrade
pip install -r requirements/dev.txt --upgrade
pip install -e .
```

17. Get yarn going

```sh
npm install -g yarn
```

18. Yarn install

P.S. this one is slow

```sh
yarn install
```

19. Initialize Database

```sh
kolibri manage migrate
```

20. Run the devserver (congrats)

P.S. this one is also slow

```sh
yarn run devserver
```

Go to http://127.0.0.1:8000/
