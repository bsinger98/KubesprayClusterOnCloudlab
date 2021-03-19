Step-by-step instructions to easily deploy kubespray cluster on Cloudlab. 

There is also support for deploying the Sockshop microservice application onto the cluster and simulating user activity.

----
NOTE: SSH connections to Cloudlab time out all the time. If the terminal looks frozen, just start a new one, navigate to the correct directory, and keep following the steps. Usually the command kept running in the background.

# Instructions
1. Create new experiment on Cloudlab using the “small-lan” profile (3 hosts) and Wisconsin cluster (if Wisconsin cluster is full, feel free to use other clusters)
    * Should boot up quickly (within a few minutes)
2. Clone this repo and move into the corresponding directory
    1. Run: `git clone https://github.com/fretbuzz/KubesprayClusterOnCloudlab.git`
    2. Run: `cd KubesprayClusterOnCloudlab`
3. Run: `bash setup_kubespray_prereqs.sh`
4. Manually setup passwordless-SSH:
    1. `cd ~/.ssh/`
    2. Store your cloudlab private key in tempkey.pem. Do this by first creating a new file called tempkey.pem (if it doesn't already exist). Then, get your cloudlab private key by going to https://www.cloudlab.us/, pressing “Download Credentials”, and copy-pasting the whole file up to and including the “END RSA PRIVATE KEY” line into tempkey.pem. 
    3. Put your Cloudlab public key in tempkey.pub (can get from https://www.cloudlab.us/ssh-keys.php’)
5. Move back to the relevant directory: `cd ~/KubesprayClusterOnCloudlab`
6. Run: `bash deploy_kubespray.sh`. At some point you will be asked for the phasephrase for `.ssh/tempkey.pem`. This is the password to your Cloudlab profile. If the password was correct, it will output “Identity added:...". If any y/N prompts shows up, respond: `y`.
   NOTE: IF this command succeeds, you should see a ton of ansible output.
7. Setup InfluxDB integration with Prometheus (this is one way to get the time series data)
8. \[If you want to deploy sockshop\]Run: `bash deploy_sockshop.sh`
