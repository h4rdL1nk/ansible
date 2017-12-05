#Environment build
pip install --upgrade pip molecule docker

#Role initialization
molecule init role -d docker -r test

#Add scenario to role
cd /test-vagrant
molecule init scenario --role-name test-vagrant --scenario-name docker --driver-name docker 
