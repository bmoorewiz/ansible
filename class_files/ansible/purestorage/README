* Connect to one of the two following lab systems via SSH (Putty)
  * Server #1 - engineeringsummit1.datalinklabs.local (10.207.61.101)
  * Server #2 - engineeringsummit2.datalinklabs.local (10.207.61.102)
  * Username: root
  * Password: D@talink1
* Create the following directory
  * # mkdir -pv /root/your_username>
  * Ex. # mkdir -pv /root/dburkland
* Copy all of the class files into your directories
  * # /bin/cp -rvf /root/class_files/* /root/<your_username>/
  * Ex. # /bin/cp -rvf /root/class_files/* /root/dburkland/
* Start an instance of the automation container image
  * # docker run --name <your_username> -d -v "/root/<your_username>/ansible:/etc/ansible/playbooks" -v "/root/<your_username>/terraform:/etc/terraform" --restart=always -t dburkland/automation:latest /bin/bash
  * Ex. # docker run --name dburkland -d -v "/root/dburkland/ansible:/etc/ansible/playbooks" -v "/root/dburkland/terraform:/etc/terraform" --restart=always -t dburkland/automation:latest /bin/bash
* Login to the container instance
  * # docker exec -ti <your_username> /bin/bash
  * Ex. # docker exec -ti dburkland /bin/bash
* Change to the purestorage ansible playbook directory
  * # cd purestorage
  * # ls
* Change the name of the volumes you are looking to create to reflect your Username
  * # sed -i 's/testvol/<your_username>/g' *.yml
  * Ex. # sed -i 's/testvol/dburkland/g' *.yml
* Create the test volumes on the lab Pure array using ansible
  * # ansible-playbook 1_ansible_pure_playbook.yml
* On your workstation, open up a browser window and point it to the lab Pure Storage array
  * URL: https://e7pure0fa01.datalinklabs.local
  * Username: pureuser
  * Password: pureuser
* Verify the new test volumes were created by navigating to Storage -> Volumes within the Pure array web interface. You should see the new volumes under the "Volumes" section of the page.
* Create a test snapshot of the recently created volumes on the lab Pure array using ansible
  * # ansible-playbook 2_ansible_pure_playbook.yml
* From the Pure web interface, you should see the new volume snapshots under "Volume Snapshots"
* Once you have verified snapshots of the recently created volumes have been created, let's now create a clone of each based on those snapshots.
  * # ansible-playbook 3_ansible_pure_playbook.yml
* From the Pure web interface, you should see the new clone (clone_<your_username>) volumes under "Volumes"
* Once you have verified the clone volumes were created, it is now time to cleanup everything we provisioned
  * # sed -i 's/cleanup: false/cleanup: true/g' 3_ansible_pure_playbook.yml
  * # ansible-playbook 3_ansible_pure_playbook.yml
* From the Pure web interface, verify the recently created objects are no longer present
* That concludes this lab exercise
