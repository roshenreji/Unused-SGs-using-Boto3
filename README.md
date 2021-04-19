# Finding List of all Unused Security Groups

### Make sure your aws is configured with your system with the help of AWS Cli
### Create a file and copy the following contents and paste it there
````
import boto3 
ec2 = boto3.client("ec2")

all_instances = ec2.describe_instances() 
all_sg = ec2.describe_security_groups()

instance_sg_set = set()
sg_set = set()

for reservation in all_instances["Reservations"] :
  for instance in reservation["Instances"]: 
    for sg in instance["SecurityGroups"]:
      instance_sg_set.add(sg["GroupName"]) 


for security_group in all_sg["SecurityGroups"] :
  sg_set.add(security_group ["GroupName"])

idle_sg = sg_set - instance_sg_set
print (idle_sg)
````
### Run the code in terminal
````
python <nameOfTheFile.py>
````

## Output
````
{'default', 'sample'}
````