# Unencrypt-an-encrypted-EBS-volume

## Description

In this article, I will help you to unencrypt an encrypted EBS volume. We would able to encrypt an EBS volume when we creating the volume. Encrypting would enable an extra safty to the volume. If we lost the key used for the encryption, it would be more difficult to keep the instance. So here am mentioning the steps to unencrypt an encrypted EBS volume.

## Table of Contents

1. Stop the instance which have the encrypted volume.
2. Dettaching the volume from the instance.
3. Creating the new rescue instance.
4. Create a new unencrypted volume with the same configuration and availability zone as the original volume.
5. Attaching both volumes to rescue instance.
6. Copy the contents from encrypted volume to new uncrypted volume.
7. Dettaching the volumes from instance.
8. Attaching the new volume to old instance.
9. Starting the Instance.


### 1-Stop the instance which have the encrypted volume

First we are going to stop the instance wich have the encrypted volume. The instance Name tage is "Instance-encrypted root volume". stoping the instance.
![image](https://user-images.githubusercontent.com/100775801/161931244-cac97766-bf35-4dc2-8306-52af69d8276b.png)

### 2-Dettaching the volume from the instance

Now we are going to dettach the instance encrypted volume. For that go the volume section, select the volume and click detach volume from actions.
Please confirm the volume ID before detaching.

![image](https://user-images.githubusercontent.com/100775801/161932089-67207051-876e-4a34-8497-fa78b447c18b.png)

### 3-Creating the new rescue instance

In this step we are creating a new rescue instance with same OS and same availability zone of first instance. 

![image](https://user-images.githubusercontent.com/100775801/161935399-eecf01ac-a899-4b6e-a0a1-02b5a9660746.png)

Here I have created new rescue instance with same availability zone. New instance name tag is "Instance- rescue"

### 4-Create a new unencrypted volume with the same configuration and availability zone as the original volume

Now we are going to create a new volume with the same size of old encryped volume in the same availability zone.

For that go to volume section and click create volume.
![image](https://user-images.githubusercontent.com/100775801/161936026-56a125d4-539e-42c7-81ef-17e3f2bc1c81.png)

Provide the same volume size and select the same availability zone.

![image](https://user-images.githubusercontent.com/100775801/161936420-803a5cfa-f8c4-4cc1-843f-cbba0870c63b.png)

Untick the Enctypted section and add a name tag for the volume. 

![image](https://user-images.githubusercontent.com/100775801/161936783-8d75e5a1-1282-4ad8-93dd-0affd09c0213.png)

### 5-Attaching both volumes to rescue instance

Now we have 2 detached volume first one is encrpted volume of the instance and second one is newly created volume with same size and availability zone.

![image](https://user-images.githubusercontent.com/100775801/161937226-019ba9ae-1704-400c-a25a-45b6bb41968a.png)

Now we are attaching bothe these volumes to rescue instance. 
For that select the volume and select attach volume from action section.
 
 ![image](https://user-images.githubusercontent.com/100775801/161937855-46e2bd22-c9c4-4719-9f15-b94feec4eec0.png)

Select the rescue instance and click attach volume.

![image](https://user-images.githubusercontent.com/100775801/161938161-8690a3c2-a759-41d6-a48e-9e5cc678c7b1.png)

Now the attached volume is /dev/sdf

Next we ara attaching the newly created volume by following the same setps.

![image](https://user-images.githubusercontent.com/100775801/161938822-1cbcefa1-3d9d-4388-bdea-32e9541f09da.png)

The second attached volume is /dev/sdg


### 6-Copy the contents from encrypted volume to new uncrypted volume

Now SSH to rescue instance using the keypair and run command lsblk to know the details of attached volumes.

![image](https://user-images.githubusercontent.com/100775801/161940020-fa50fd93-edf8-4cd4-9fd3-04b41ad67ae3.png)

Here we can see the newly attached two volumes.
Next we are going to copy the contenst from encrypted volume to unencrypted volume by using "dd"

~~~
 dd if=/dev/xvdf of=/dev/xvdg bs=4096 status=progress
~~~

~~~
dd if=/dev/xvdf of=/dev/xvdg bs=4096 status=progress
8574980096 bytes (8.6 GB) copied, 133.172507 s, 64.4 MB/s
2097152+0 records in
2097152+0 records out
8589934592 bytes (8.6 GB) copied, 134.369 s, 63.9 MB/s
~~~

### 7-Dettaching the volumes from instance

After coping the contents to new uncrypted volume now we are going to detach previously attached volumes from the rescue instance.
For detaching the volume, go to volume section and select the volume, click detach volume from actions.

![image](https://user-images.githubusercontent.com/100775801/161945077-fff88d59-69cb-4378-92fd-9d87e1d6842f.png)

### 8-Attaching the new volume to old instance

After detaching the volume we are going to attach the newly created volume Name tag "New-unencrypted volume" which have the uncrypted contents to the old instance.
For that select the volume and click on attach volume. Select the old instance in stopped state and click attach volume.

![image](https://user-images.githubusercontent.com/100775801/161945933-cd603c54-de3d-4455-b1c5-f39298f8698b.png)

### 9-Starting the Instance

Go to EC2 dashboard and start the stopped instance.

![image](https://user-images.githubusercontent.com/100775801/161946348-bcd9e266-0150-4c31-bc39-d2420dd13813.png)

We can check the volume status under "Storage".

![image](https://user-images.githubusercontent.com/100775801/161946559-3891c2f9-f597-4d16-a320-19b5eb187920.png)

## Conclusion

In this tutorial we discussed how to unencrypt an encrypted volume. The goal is to get you started on using this methode if we dont have the key as it is cheap and easy to do.

### ?????? Connect with Me

<p align="center">
 <a href="https://www.instagram.com/itz__me_omkar/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/sanu-das-t-3722891b5"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a> 





