# ***Access Control In Network Security***
**Access control** in security specifies that only authorized people can access the data or modify it. Not everyone can access it, but only those who are authorized. 

---
#### ***Authentication:***
The first stage of access control defines the identity of users.
For example, when you are trying to log in to your bank account, it asks for your username and password to verify your identity and ensure that you are an authenticated user. 

Authentication ensures that the user is indeed who they claim to be, but it does not determine what that user is allowed to do within the system.

Authentication can be achieved through different factors:
- Smart card
- One-Time Password (OTP)
- Security Question

---
#### ***Authorization:***
The stage that comes next after the authentication stage. After the user authentication process is successful, what privileges does the user have?
Authorization is not about defining identity, but permissions.
Authentication is like "Who are you?" while Authorization is "What are you allowed to do?"

For example, when two users logged in successfully to the same banking system.
**One** of them is a normal customer who can view their balance, transfer money, and pay bills.
**The other** one is a system administrator who can approve loans, manage customer accounts. I think you can see the difference now! *Each of them has its own permissions.*

Authorization can be managed in different ways:

- **Discretionary Access Control (DAC)**: Access is based on the identity and the permissions of the user.
	For example, in Windows, if you created a text file, you are now the owner, and you can specify who can read or write.

- **Mandatory Access Control (MAC)**: Each data has its own Sensitivity level, and no one can access it except they have the same level of security.

- For example, A military organization has data with a **_"Top Secret"_** sensitivity level. Now, if a user has a **_confidential_** security level, then it will not be allowed for him to access the data, even if he is an admin.

- **Role-Based Access Control (RBAC):** Access based on the user role.

For example, a company has:

1. HR Role => can access the employees' data.

2. Admin Role => can add/delete users and manage the system.

3. Finance Role => Can see employees' accounts and the financial reports.

And so on ….

---
#### ***Access:***
Here is where the game actually starts. After you enter your username and password and the system ensures that you are authenticated and authorized, the system will allow you access to the data or stop you based on the authorization process.

For example, when you successfully log in to your bank account, the **Authentication stage** is done. After that, you are trying to see your balance and successfully see it!

It's actually because you are authorized to do that; now you're trying to see another user's balance. Unfortunately, you can't! Why? Because you are not allowed to.

---
#### ***Manage:***
Now, after we talked about authentication and authentication and authorization, how can we control and manage these processes?

For example, when a new employee comes to the company, the system admin should create an account for them and set the permissions based on their role: HR, Sales, or IT.

Also, if an employee has left the job or been fired, should their account be locked or deleted

----
#### ***Audit:***
Actually, this stage is very critical. It is where the activity of the user is actually being recorded. But why? So you can see if there is any suspicious activity, such as:

- Too many failed login attempts => it may be a hack attempt
- The user is trying to access data that is not allowed to
- Or maybe there is a user who has more privileges than they actually should have

----
### Why does Access Control really matter? 

#### **Protecting the sensitive data**
If you have a large company, you should protect your clients' data, such as:
- Names, phone numbers, or banks' accounts
- Medical information (medical records)
- Company's financial and management information

So, access control ensures that only authorized people can access this data, and prevents :

- Data breaches
- Data manipulation
- Or using these data in a phishing attack or identity theft

As an example, in a communication company, the technical support can see the client's information data, so they can help them, but they can't access their paying information or credit card information because only the financial department has access to it
