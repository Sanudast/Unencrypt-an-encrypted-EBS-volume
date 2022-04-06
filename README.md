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


## 1-Stop the instance which have the encrypted volume

First we are going to stop the instance wich have the encrypted volume. The instance Name tage is "Instance-encrypted root volume". stoping the instance.
![image](https://user-images.githubusercontent.com/100775801/161931244-cac97766-bf35-4dc2-8306-52af69d8276b.png)

## 2-Dettaching the volume from the instance

Now we are going to dettach the instance encrypted volume. For that go the volume section, select the volume and click detach volume from actions.
Please confirm the volume ID before detaching.

![image](https://user-images.githubusercontent.com/100775801/161932089-67207051-876e-4a34-8497-fa78b447c18b.png)

## 3-Creating the new rescue instance

In this step we are creating a new rescue instance with same OS and same availability zone of first instance. 

![image](https://user-images.githubusercontent.com/100775801/161935399-eecf01ac-a899-4b6e-a0a1-02b5a9660746.png)

Here I have created new rescue instance with same availability zone. New instance name tag is "Instance- rescue"

## 4-Create a new unencrypted volume with the same configuration and availability zone as the original volume

Now we are going to create a new volume with the same size of old encryped volume in the same availability zone.

For that go to volume section and click create volume.
![image](https://user-images.githubusercontent.com/100775801/161936026-56a125d4-539e-42c7-81ef-17e3f2bc1c81.png)

Provide the same volume size and select the same availability zone.

![image](https://user-images.githubusercontent.com/100775801/161936420-803a5cfa-f8c4-4cc1-843f-cbba0870c63b.png)

Untick the Enctypted section and add a name tag for the volume. 

![image](https://user-images.githubusercontent.com/100775801/161936783-8d75e5a1-1282-4ad8-93dd-0affd09c0213.png)

## 5-Attaching both volumes to rescue instance

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

The second attached volume is






