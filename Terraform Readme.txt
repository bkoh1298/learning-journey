How to run terraform in Ubuntu Workstation to deploy vm instances for GCP.

0. Login to Virtual-box / login to ubuntu
1. @Safari browser , search Google for terraform download
2. search for Linux -- right mouse click, select "copy link"
3. goto to ubuntu/terminal , run command 

$ pwd                    #make sure you see the path eg:/servername/home/
$ mkdir terraform        #so terraform is now at /servername/home/terraform
$ wget {paste the copied link here}

4. run command 
$ unzip downloaded-filename

5. Next , inside Safari (ubuntu machine), goto http://cloud.google.com/gcp
login using your google account

6. Goto IAM & Admin -> Service Account ->  blahblah-compute@developer.gserviceaccount.com  
a. click on it and "Create New Key"
b. select json 
c. save to the location /servername/home/terraform

7. run command 
$  export GOOGLE_APPLICATION_CREDENTIALS=[paste json filename here without the [] bracket ]

8. create main.tf file inside /servername/home/terraform
content of main.tf should be like this
++++++++++++++++++++++++++++++++++++++++++
provider "google" {
	project	= "name of your project id"
	region	= "asia-southeast1"
	zone	= "asia-southeast1-a"
}

resource "google_compute_instance" "terraform-vm" {
	name = "vm-instance88"
	machine_type = "f1-micro"

	boot_disk {
	 initialize_params {
		image = "debian-cloud/debian-9"
	 }
}
	network_interface {
		network = "default"
}
}
++++++++++++++++++++++++++++++++++++++++++++++

9. run command
$ ./terraform init
$ ./terraform plan
$ ./terraform apply

That's it :D 