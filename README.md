terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}
provider "aws" {
  region = "eu-west-2"
  profile = "user101"
}
resource "aws_s3_bucket" "mybucket" {
  bucket = "devops-yamu-2023"

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}
resource "aws_s3_object" "obj1" {
key = "mystudents.txt"
source = "./students.txt"
etag = filemd5("./students.txt")
bucket = "${aws_s3_bucket.mybucket.id}"
}

