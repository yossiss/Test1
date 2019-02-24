install nginx:

yum install nginx
systemctl enable nginx ( to up on boot )
systemctl restart nginx

go to:
cat /etc/nginx/nginx.conf #### to check where the html.index is locate
vi /usr/share/nginx/html/html.index #### Change the login message to Hello Tunity

ifconfig got IP:
image.png



image.png




Terraform Part:

Terraform installation:
curl -O https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip


 echo $PATH
/sbin:/bin:/usr/sbin:/usr/bin
unzip terraform_0.11.1_linux_amd64.zip -d /usr/bin/



mkdir terraform-templates && cd terraform-templates


Yosi Shaer‏ <yosi1232@gmail.com‏>
9:21 (לפני 31 דקות)
אני

need to create config,tf file as follow:
provider "docker" {
  host = "tcp://docker:2345/"
}
resource "docker_image" "nginx" {
  name = "nginx:1.11-alpine"
}
resource "docker_container" "nginx-server" {
  name = "nginx-server"
  image = "${docker_image.nginx.latest}"
  ports {
    internal = 80
  }
  volumes {
    container_path  = "/usr/share/nginx/html"
    host_path = "/<Path Where Config Locate>/config.tf"
    read_only = true
  }
}



before run this need to run the command:
terraform init  (Initialize a Terraform working directory)

then use the command:
terraform plan
terraform apply ( To create the new container )

the result should be:
image.png
 
