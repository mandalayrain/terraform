provider "aws" {
  region = "us-east-1"
}

resource "aws_security_group" "instance" {
  name        = "mandalay security group"
  description = "Allow all 8080"

  ingress {
    from_port   = "${var.server_port}" 
    to_port     = "${var.server_port}" 
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "mandalayrain" {
  ami           = "ami-40d28157"
  instance_type = "t2.micro"
  vpc_security_group_ids = ["${aws_security_group.instance.id}"]

  user_data = <<-EOF
              #!/bin/bash
              echo "Hello, World" > index.html
              nohup busybox httpd -f -p "${var.server_port}" &
              EOF

  tags {
    Name = "mandalay"
  }
}
