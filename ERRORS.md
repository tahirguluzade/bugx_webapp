#Explanation of errors and fixing them

error 1:

<kbd>dnf config-manager --set-enabled crb</kbd>
  Error: No matching repo to modify: crb.
when facing above error run following:
<kbd>dnf -y config-manager --set-enabled powertools</kbd>

error 2:

while running following command <kbd>su -c 'bundle install' brew-user</kbd>, the most probably you will get an error about permission

for solving this,
manually add <kbd>export GEM_HOME=$HOME/.gem</kbd>, <kbd>export PATH=$PATH:$HOME/.gem/bin</kbd>, <kbd>exportPATH=$PATH:$HOME/.gem/ruby/<version>/bin</kbd> to your .bash_profile

and also give permission to <kbd>sudo chown -R YOURUSER:YOURUSER path(where permissin needed shows in error)</kbd>
