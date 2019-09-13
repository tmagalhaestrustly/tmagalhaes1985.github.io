# Creating Microsoft CA templates

From my experience, a majority of our customers are using Microsoft for their internal CA. One thing I wanted to document for everyone is how to properly create Microsoft CA templates to sign the Certificate Signing Requests (CSRs). There are a few different templates to create, depending on what certificates you are replacing.

## Template for Web Server SSL certificate

1. First, log into your CA server as an administrator and navigate to Start and type certmpl.msc This will open up the Certificate Templates Console where you can manage the various templates for which you sign your certificates.

    ![Image: SSL Template 1](/mdwiki/pages/kb/microsoft/adcs/img/ssl1.png)

2. Next, you will clone a template to use, the one that most closely matches VMware’s requirements is the Web Server template. Right click on the template and select Duplicate Template. When prompted, you will select Windows Server 2003 enterprise. I noticed that when I clone a template as Windows 2008 it doesn’t show up when signing the certificate.

    ![Image: SSL Template 2](/mdwiki/pages/kb/microsoft/adcs/img/ssl2.png)

    ![Image: SSL Template 3](/mdwiki/pages/kb/microsoft/adcs/img/ssl3.png)

3. Provide a Template display name. Then click on the Extensions tab.

    ![Image: SSL Template 4](/mdwiki/pages/kb/microsoft/adcs/img/ssl4.png)

4. Click Application Policies then click Edit. Highlight Server Authentication and select Remove then hit OK.

    ![Image: SSL Template 5](/mdwiki/pages/kb/microsoft/adcs/img/ssl5.png)

5. Select Key Usage then click Edit. Click the checkbox next to Signature is proof of origin (nonrepudiation) then hit OK.

    ![Image: SSL Template 6](/mdwiki/pages/kb/microsoft/adcs/img/ssl6.png)

6. Click OK again to finish the template creation. You should now see a new template created. If you are not creating a template for VMCA as a subordinate CA, go ahead and skip to the very bottom to assign the templates for usage.

    ![Image: SSL Template 7](/mdwiki/pages/kb/microsoft/adcs/img/ssl7.png)

## Template for Subordinate CA

1. Duplicate the Subordinate Certification Authority, and ensure to use a Windows 2003 template as in the previous section. Provide a Template Display Name and .. Important: make sure to check in Publish certificate in Active Directory

    ![Image: Subordinate CA 1](/mdwiki/pages/kb/microsoft/adcs/img/sub1.png)

    ![Image: Subordinate CA 2](/mdwiki/pages/kb/microsoft/adcs/img/sub2.png)

2. Click on the Extensions tab and then edit Key Usage. Ensure Digital Signature, Certificate signing, CRL signing and Make this extensions critical are checked. By default, these should already be checked, but it’s important to confirm. Finally, go ahead and click OK to create the template.

    ![Image: Sub CA 3](/mdwiki/pages/kb/microsoft/adcs/img/sub3.png)

## Assign template for usage

Finally, you will need to assign these templates for use. This will need to be done for both the templates you have created. If you don’t do this step, you will not be presented with the templates you created as an option when signing the CSR files. To complete this step you will need to open the Certificate Server gui by navigating to **Start** and typing **certsrv.msc**. Once that is open, expand out the CA Server and right click Certificate Templates and select **New -> Certificate Template to Issue**.

![Image: Assign Template 1](/mdwiki/pages/kb/microsoft/adcs/img/assign1.png)

Select the certificates that you created, then click **OK**. You are able to select multiple certificates so feel free to do them both in one step.

![Image: Assign Template 2](/mdwiki/pages/kb/microsoft/adcs/img/assign2.png)