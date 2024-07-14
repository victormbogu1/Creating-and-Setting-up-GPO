# Group Policy Console Management (GPOs)
## Description
This project outlines the essential setup steps for managing an on-premises Active Directory Group Policy Management (GPOs). The first part involves creating and setting up GPOs, and the second part focuses on implementing and testing those GPOs, continuing from the previous project. This project is designed to help you understand how these systems are set up, as someone in the company typically manages the Active Directory Group Policy. This involves setting account lock policy to prevent brute force attacks and other examples will be showned as well

Building on the previous project, this will involve the 1000+ users created with Azure Active Directory. It includes setting up a Microsoft Server to run Active Directory and configuring a Domain Controller to manage a domain. Note that this lab won't show the installation of GPO since it is automatically included when installing AD.

This lab replicates a business environment setup. The required tools include Microsoft Server 2019 ISO, Windows 10 Enterprise ISO, and VirtualBox. Note that the installation of VirtualBox and the client machine won't be displayed here, but I will provide the download links below as usual
## Languages and Utilities Used
  + Window Server
  + Active Directory
  + Group Policy Management Console (GPMC)
  + CMD
## Environments Used
  + VirtualBox
  + Microsoft Server 2019
  + Windows 10 Enterprise
## Links
  + [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  + [Windows 10 ISO](https://www.microsoft.com/de-de/evalcenter/download-windows-10-enterprise/)
  + [Windows Sever 2019](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019)
  + [Powershell script](https://techcommunity.microsoft.com/t5/itops-talk-blog/powershell-basics-how-to-force-azuread-connect-to-sync/ba-p/887043)
## Program walk-through

[![Untitled-Diagram-drawio.png](https://i.postimg.cc/zGVqZ8kZ/Untitled-Diagram-drawio.png)](https://postimg.cc/fVnGY4FB)

As shown in the diagram above, the Group Policy Management console provides a centralized system where you can manage all group policy settings. This involves an administrator controlling the management of users and computers.

# GPO Types

As seen in the picture below, there are two types: Computer Configuration and User Configuration.

Computer Configuration: Applies settings to the local computer and does not change per user. This is limited to settings that affect the computer itself, not the users logging into it.

User Configuration: Applies settings to users on the local machine and any new users in the future on this local computer. This configuration only affects users.

It is crucial to understand where to apply each policy in the group policy. While it can be confusing at first, familiarity makes it easier to apply. The frequency with which a company applies policies also plays a role.

Within both User and Computer Configuration, there are different settings under Policies and Preferences. Expanding these configurations reveals more options and settings. Learning this can be challenging due to the multitude of settings available. Understanding the difference between Policies and Preferences is important for creating a GPO effectively.

[![Screenshot-2024-07-13-115519.png](https://i.postimg.cc/s2jqdczB/Screenshot-2024-07-13-115519.png)](https://postimg.cc/18dJDDfP)

# Types of Group Policy Settings

The diagram provides a well-detailed explanation of the group policy types: 


[![Untitled-Diagram-drawio-1.png](https://i.postimg.cc/SxJYT02j/Untitled-Diagram-drawio-1.png)](https://postimg.cc/Hr1LnhtC)

# Applying and Testing GPO

For this task, I'll be setting up three GPOs for hands-on activity, which will be applied to the 1000 bulk users created previously. These three GPOs will involve:

Creating wallpapers for the 1000 users.
Restricting user access to the control panel on client machines.
Securing computers from brute force attacks by setting an account lockout policy for users.
I'll begin by creating and configuring each GPO, starting with the wallpaper for all client machines used by the users. The steps for implementing the other GPOs will follow the same process.

Before creating the wallpaper policy, I had to configure the share access on the image, as shown below

[![Screenshot-2024-07-13-162226.png](https://i.postimg.cc/KzL4CVTb/Screenshot-2024-07-13-162226.png)](https://postimg.cc/xJf0z6gp)

Next, I granted full access to authorized users

[![Screenshot-2024-07-13-164349.png](https://i.postimg.cc/VsqdRx1B/Screenshot-2024-07-13-164349.png)](https://postimg.cc/9zfmXNDr)

[![Screenshot-2024-07-13-123135.png](https://i.postimg.cc/yxkRtWvg/Screenshot-2024-07-13-123135.png)](https://postimg.cc/rR2zty6M)

Creating the wallpaper policy as demonstrated below:

[![Screenshot-2024-07-13-123247.png](https://i.postimg.cc/B6yb8pBb/Screenshot-2024-07-13-123247.png)](https://postimg.cc/r01M3Sb2)


[![Screenshot-2024-07-13-123445.png](https://i.postimg.cc/L8MD7KZ9/Screenshot-2024-07-13-123445.png)](https://postimg.cc/dL4GkfBp)

Since this is a wallpaper policy, I have to integrate it from the User Configuration and implement it via Policies, not Preferences, as explained above

[![Screenshot-2024-07-13-123747.png](https://i.postimg.cc/T3q0v7rr/Screenshot-2024-07-13-123747.png)](https://postimg.cc/yDxcFTpd)

Next, I enabled the wallpaper policy to ensure it is replicated across all client machines by copying the shared path of the image

[![Screenshot-2024-07-13-163024.png](https://i.postimg.cc/ZqwLCWsn/Screenshot-2024-07-13-163024.png)](https://postimg.cc/gw6h72Wb)

Next, I need to enforce the group policy. By default, Windows refreshes GP settings every 90 minutes, with a random offset of up to 30 minutes. To ensure immediate application, I'll force the policy update

[![Screenshot-2024-07-13-141844.png](https://i.postimg.cc/wMwtkNJR/Screenshot-2024-07-13-141844.png)](https://postimg.cc/kRtXJBT7)

Now the policy has been successfully implemented for all client users joined to the DC domain

[![Screenshot-2024-07-13-165049.png](https://i.postimg.cc/zf4Vt5Vp/Screenshot-2024-07-13-165049.png)](https://postimg.cc/Jycr0f3B)

Next, the policy to be integrated will restrict users access to the Control Panel to prevent them from making unauthorized changes. As mentioned earlier, the steps for configuring this policy are identical to those for setting up the wallpaper. Therefore, we'll navigate to the User Configuration to enforce restrictions on users via policy, as shown below

[![Screenshot-2024-07-13-124935.png](https://i.postimg.cc/x86QZy6Y/Screenshot-2024-07-13-124935.png)](https://postimg.cc/jnnBwNVk)

Now you can see that the user aaaba has been successfully restricted

[![Screenshot-2024-07-13-142138.png](https://i.postimg.cc/nrhbq9pW/Screenshot-2024-07-13-142138.png)](https://postimg.cc/xJh42CkG)

Next configuring account lockout settings to prevent brute force attacks is mandatory in all companies to safeguard against unauthorized access to resources

[![Screenshot-2024-07-13-125624.png](https://i.postimg.cc/4NFZbPKQ/Screenshot-2024-07-13-125624.png)](https://postimg.cc/CzDWwjsR)

I configured the threshold and set it to 3. The threshold defines the number of failed sign-in attempts, and it's recommended to keep it as low as possible to prevent brute force attacks. This reduces the chances of credentials being compromised. The specific threshold may also depend on your company's security policy, but typically, a threshold of 3-5 attempts is commonly used

[![Screenshot-2024-07-13-152448.png](https://i.postimg.cc/fRtsHdmn/Screenshot-2024-07-13-152448.png)](https://postimg.cc/CRg95zcm)

Next, I tested the configuration, and I couldn't log in because I had exceeded the sign-in attempt limit

[![Screenshot-2024-07-13-153744.png](https://i.postimg.cc/SxBhHKfX/Screenshot-2024-07-13-153744.png)](https://postimg.cc/PCQ9wTch)

I went to the domain controller (DC) to confirm that the account for user aaaba has been locked. To unlock it, you can click the checkbox as mentioned earlier. This action may vary depending on the policy in place

[![Screenshot-2024-07-13-154028.png](https://i.postimg.cc/bv1hPjmm/Screenshot-2024-07-13-154028.png)](https://postimg.cc/SXQ5LHF9)

For final verification to ensure all policies have been applied, I used the command `gpresult /r` to confirm their implementation

[![Screenshot-2024-07-13-151951.png](https://i.postimg.cc/B6G1Z44b/Screenshot-2024-07-13-151951.png)](https://postimg.cc/Z9VqVk9z)


