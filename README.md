<h1>Network Security Groups and File Sharing</h1>

> [!Important]
> You'll need a Domain Controller with Active Directory installed and Client VM. If you need assistance setting these up, refer to the guide for [Active Directory Configuration](https://github.com/EMoniSmall/ad-configure)

<h2>Expectations 🤔</h2>

- Gain an understanding of File Shares

- Create and test File Shares

- Gain an Understanding of Security Groups

- Create and test Security Groups

<h2>File Shares 📂</h2>

> [!Note]
> What are File Shares?
> File shares are files and folders on computers and networks that are stored and made accessible to multiple users. It allows users to share documents, photos, videos and other types of files. They are often used for businesses and organizations. Examples of this can include sharing Spreadsheets that are read only or visitors also have read/write access.

Step 1: Log into DC-1 Remote Desktop as your Admin Account. (John_Admins in this example)

Step 2: Log into Client-1 as a random normal user you've created during the [active directory tutorial](https://github.com/EMoniSmall/ad-configure). 

> [!Note]
> You can choose a normal user profile by going to DC-1 > Active Directory Users and Computers > mydomain.com > _EMPLOYEES. In this example, Goku.Pubob will be used. When logging into Client-1 via remote desktop. Your username will be mydomain.com\goku.pubob and password should be defaulted to Password1. 

![mstsc_PfYZRKvd48](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/f59d92fe-9269-4a85-92de-6b45e2e061f2)

Step 3: On DC-1 Remote Desktop, create 4 folders under your C Drive. They can be named anything you like but for this example, they will be named "read-access", "write-access", "no-access", and "accounting."

![image](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/4146363c-9c7e-4746-adcc-04dc1b850da6)

Step 4: Right-click Read-Access > Properties > Sharing > Share... > Type Domain Users > Add. Make sure the permission level is set to Read-only.

Step 5: Right-click Write-Access > Properties > Sharing > Share... > Type Domain Users > Add. Make sure the permission level is set to Read/Write.

Step 6: Right-click No-Access > Properties > Sharing > Share... > Type **Domain Admins** > Add. Make sure the permission level is set to Read/Write. 

![mstsc_pfJxwFvben](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/f04e0396-e30c-4efa-a297-3beb1d64e771)

> [!Note]
> Accounting folder will be skipped for now.

<h3>Attempting to Access the File Shares as a Normal User</h3>

Step 1: Switch to Client-1 Remote Desktop and open a File Explorer. 

Step 2: In the search bar, type in \\dc-1. You should see the read, write, and no-access folders inside.

![image](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/b856a307-42a2-4cfd-99e8-02d04a81715f)

Step 3: You can attempt to experiment in the folders and see which folders you're allowed to read, create files, or even access at all. 

<h2>Creating a Network Security Group</h2>

> [!Note]
> For File sharing, a network security group, controls the access of users by restricting or allowing access to authorized users or systems. This helps prevent unauthorized access or malicious activities. This in turn enhances the security of file sharing by helping contain potential security risks and limit the impact of security incidents. 

Step 1: Return to DC-1 and open Active Directory Users and Computers. 

Step 2: Right-click mydomain.com > New > Organizational Unit and name it "Security Groups." 

Step 3: Under Security Groups, right-click > new group > name it Accountants.

Step 4: Back in DC-1's File Explorer, right-click the accounting folder you created earlier > Properties > Sharing > Share... > Type Accountants > Add. Make sure the permission level is set to read/write. 
 
![mstsc_QZLElnNrgt](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/e1dbfa9e-0eef-4c46-b93e-c3938bb4f361)

Step 5: Return to Client-1 and attempt to access the accounting folder. You'll notice access is denied because your normal user profile currently is not in the Accountants Security Group.

Step 6: Go back to DC-1 and open Active Directory Users and Computers > Security Groups > Accountants > Members and enter your normal user profile. In this example it is goku.pubob.

![mstsc_SHXbyuWzd4](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/a597bf3d-1f29-4d34-9054-614039c2640f)

Step 7: In Client-1, you should now be able to access the accounting folder. You may need to log out and log back into Client-1 for the changes to take effect.


