Install git on your staging server - sudo apt-get install git

Install docker - sudo apt-get install docker.io

Install fig - curl -L https://github.com/docker/fig/releases/download/1.0.1/fig-uname -s-uname -m> /usr/local/bin/fig; chmod +x /usr/local/bin/fig

Pull repo from server git remote add origin git@github.com:5aket/dungvisor.git

fig build

fig up
