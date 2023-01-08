# bugx_webapp

#Perform commands as a root user

- [ ] #install build dependencies, build env and finally install ruby 
dnf config-manager --set-enabled crb	#to enbale powertools for libyaml-devel
- [ ] yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel
cd ~
git clone https://github.com/rbenv/rbenv.git
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/rbenv/bin:$HOME/.rbenv/bin:$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
yum install perl -y
rbenv install 2.7.7
rbenv global 2.7.7
yum install rubygem-bundler -y

#Deploy app
useradd brew-user
usermod -aG root brew-user
git clone git@github.com:EshginGuluzade/bugx_wepapp.git
cd /root/bugx_wepapp/
su -c 'bundle install' brew-user
bundle exec jekyll serve --host 0.0.0.0

#Add as systemd service [Optional]
#vim /etc/systemd/system/bugx.service
[Unit]
Description=Bugx-webapp
Wants=network-online.target
After=network-online.target

[Service]
User=root
Group=root
Type=simple
WorkingDirectory=/root/bugx_wepapp
ExecStart=/bin/sh -c "/root/.rbenv/shims/bundle exec jekyll serve --host 0.0.0.0"

[Install]
WantedBy=multi-user.target

systemctl daemon-reload
systemctl enable bugx
systemctl restart bugx
