# Define the provider
provider "aws" {
  region = "us-east-1"
}

# Create a security group for the RDS instance
resource "aws_security_group" "rds_sg" {
  name        = "rds_sg"
  description = "Allow inbound traffic to RDS"

  ingress {
    from_port   = 3306
    to_port     = 3306
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # Replace with your IP range
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Create a subnet group for the RDS instance
resource "aws_db_subnet_group" "rds_subnet_group" {
  name       = "rds_subnet_group"
  subnet_ids = ["subnet-04bfe0631918db5b2", "subnet-0a0091f550a02d217"] # Replace with your subnet IDs

  tags = {
    Name = "rds_subnet_group"
  }
}

# Create the RDS instance
resource "aws_db_instance" "example" {
  allocated_storage    = 20
  storage_type         = "gp2"
  engine               = "mysql"
  engine_version       = "8.0"
  instance_class       = "db.t3.micro"
  name                 = "mydb"
  username             = "admin"
  password             = "admin@123" # Update with a secure password
  parameter_group_name = "default.mysql8.0"
  skip_final_snapshot  = true

  db_subnet_group_name = aws_db_subnet_group.rds_subnet_group.name
  vpc_security_group_ids = [aws_security_group.rds_sg.id]

  tags = {
    Name = "example-rds-instance"
  }
}
