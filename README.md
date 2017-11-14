#Environment build
pip install --upgrade pip molecule docker

#Role initialization
molecule init role -d docker -r test
