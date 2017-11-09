#Environment build
pip install --upgrade pip molecule docker-py

#Role initialization
molecule init role -d docker -r test
