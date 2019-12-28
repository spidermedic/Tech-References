### Configure SSH for Git Hosting Server
Add the following text to `.ssh/config` (.ssh should be found in the root of your user home folder):

`Host github.com
 Hostname github.com
 IdentityFile ~/.ssh/id_rsa`

### Ensure that following lines are added to `.bash_profile`, which should be found in your root user home folder:

`test -f ~/.profile && . ~/.profile
test -f ~/.bashrc && . ~/.bashrc`

### Now, add the following text to `.bashrc`, which should be found in your root user home folder:

`Start SSH Agent
#----------------------------

SSH_ENV="$HOME/.ssh/environment"

function run_ssh_env {
  . "${SSH_ENV}" > /dev/null
}

function start_ssh_agent {
  echo "Initializing new SSH agent..."
  ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
  echo "succeeded"
  chmod 600 "${SSH_ENV}"

  run_ssh_env;

  ssh-add ~/.ssh/id_rsa;
}

if [ -f "${SSH_ENV}" ]; then
  run_ssh_env;
  ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
    start_ssh_agent;
  }
else
  start_ssh_agent;
fi`

