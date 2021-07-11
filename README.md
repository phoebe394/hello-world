# hello-world
# setting up python on macOS

# Install homebrew
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

There will be a warning: "Warning: /opt/homebrew/bin is not in your PATH."
- Add Homebrew to your PATH in /Users/yourusername/.zprofile:
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/phoebeho/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"

Go to /Users/username and unhide the hidden files: Command + Shift + .
To create the .zshrc file (if not already there), type this into Terminal
touch .zshrc
Make your edits, then type this to make it available
source ~/.zshrc

# Install python
brew install python

# Making sure the python command uses newest python (not system python)
If this warning comes up:
Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /opt/homebrew/opt/python@3.9/libexec/bin

it means the when you type "python" it will use the system python and not the newest python i.e. to use python 3, you would need to type "python3" and the same for pip, you would need to type "pip3".

To fix this, you need to add the path in the warning to the top of the .zshrc file.
export PATH="/opt/homebrew/opt/python@3.9/libexec/bin:$PATH" 

Type source ~/.zshrc to activate the changes.

Check:
python --version
pip --version

# Install pyenv
brew install pyenv

Adding the following to your .zshrc will define the environment variable PYENV_ROOT.
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc

# Install python in the pyenv
Check which versions are available by typing 
pyenv install -l

Install latest version:
pyenv install 3.9.6

Show all python versions in your system:
pyenv versions

Set the global python version:
pyenv global 3.9.6

Verify the active version:
pyenv version

# Creating virtual environments
Install pyenv-virtualenv:
brew install pyenv-virtualenv

Run the following to add to .zshrc:
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

Create a virtualenv:
pyenv virtualenv 3.9.6 py396

Activate virtualenv:
pyenv shell py396


# Use pyenv python every time we run a command in zsh
Verify which python is being used:
which python

Run:
PATH=$(pyenv root)/shims:$PATH

Now check again which python is being used:
which python

Add this line to zshrc to make it a permanent change:
echo 'PATH=$(pyenv root)/shims:$PATH' >> ~/.zshrc

#
