# Jenkins Basic Lab

## Install

Reference: https://www.jenkins.io/doc/book/installing/linux/#fedora

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/rpm-stable/jenkins.repo
sudo dnf upgrade

# Add required dependencies for the Jenkins package
sudo dnf install fontconfig java-21-openjdk
sudo dnf install jenkins
sudo systemctl daemon-reload
```

**Check version**

```bash
rpm -qi jenkins
```

**Start Jenkins**

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

**Check**
```bash
sudo systemctl status jenkins
```

## Config

```bash
# Get the initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

# Visit http://localhost:8080 to enter password

# Create first admin user (web form)
```

## Basic Lab

```bash
mkdir jenkins-lab

cd jenkins-lab

git init
```

**Add remote and push**

```bash
git remote add origin https://github.com/<your-user>/jenkins-lab.git
```

**Create a small script**

```bash
vim hello.sh
```

**Paste content**

```bash
echo "Hello from Jenkins"

date
hostname
whoami
pwd

```

**Create a `Jenkinsfile`**

```bash
vim Jenkinsfile
```

**Paste content**
```yaml
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build stage'
            }
        }

        stage('Run Script') {
            steps {
                sh './hello.sh'
            }
        }

        stage('Verify') {
            steps {
                sh 'echo Pipeline completed successfully'
            }
        }
    }
}
```

**Add, commit and push to remote repository**

```bash
git add .

git commit -m 'Initial commit'

git push -u origin main
```

## Create a Pipeline Job

From the web browser within the Jenkins UI

> New item

- `pipeline-lab`
- Select **Pipeline**
- Under Pipeline
    - Select **Pipeline script from SCM**
    - Choose: **Git**
    - Enter respository URL: `https://github.com/<your-user>/jenkins-lab.git`
    - Check correct branch to build is referenced (e.g. `main`)
    - Check that **Script Path** is `Jenkinsfile`
- Click **Save**

> Build

- Now attempt to **Build Now**
- Review the **Console Output**

