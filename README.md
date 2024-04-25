<h1>Network Security Groups and File Shares</h1>

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

<h2>Attempting to Access the File Shares as a Normal User</h2>

Step 1: Switch to Client-1 Remote Desktop and open a File Explorer. 

Step 2: In the search bar, type in \\dc-1. You should see the read, write and no-access folders inside.

![image](https://github.com/EMoniSmall/NetworkFilesConfig/assets/166156618/b856a307-42a2-4cfd-99e8-02d04a81715f)


