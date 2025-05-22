# Taitaja2025 - Module B – Implementing the Admin Panel

## Competition time 
4 hours

## Introduction

In this competition task, you will develop an application commissioned by Hobbly Technologies Ltd. The app helps users discover local hobbies and events. 

The competitor’s task is to build an admin panel for the Hobbly application, which will manage activity announcements and user accounts.

## General Description

The admin panel must be designed for a 1440px wide desktop layout and follow the client's brand guidelines.

The user interface must be straightforward and easy to use. It must support content and user management according to role-based permissions.

Judging will focus on functionality, usability, security, and code quality.

Implementation must be technically functional, clearly documented, and ready for further development.

## Requirements

**Core features**

- User registration and login (via email and password)
- Password change option in user settings
- Ability to add, edit, and delete activities (only the user's posts)
- Admin rights: manage all posts and users
- Two-step deletion process for user accounts

### User Accounts and Login
Users of the admin panel can create their accounts using a multi-step registration form.

#### Registration (3 steps, single-page flow – URL remains unchanged):
**Contact Details:**

- User’s name
- Email address
- Phone number
  
**Basic Info:**
- Upload logo (JPEG/PNG, max 2MB)
- Display name
- Description (min. 25 characters, max. 200 characters)
  
**Organisation Info:**
- Official name
- Address
- City
- Postal code
- Business ID (optional)
- Organisation type:
  - Association
  - Private
  - Limited company
  
#### Login and Security
- The email address is used as the username.
- The password must have at least eight characters and one number.
- Duplicate emails are not allowed → an error message must be shown.
- Passwords must be securely stored (e.g., bcrypt or Argon2).
- The admin panel must not be accessible without a login.
  
#### Password Change
The application creates a password when a user account is created. However, users must be able to change their passwords from within the admin panel.
When changing a password, the system must check that it meets the minimum requirements (at least eight characters and one number). If it doesn't, an error message must appear, and the password must not be changed.

#### Administrator (Admin)
- Default admin username: taitaja@hobbly.app
- Password: Taitaja123!
- Admins can manage all users and all activity posts.

### Managing Activity Announcements
Users can add, edit, and delete their hobby and activity announcements within the admin panel.
They can permanently delete or move a post to trash (soft delete).

**Form fields for adding a post:**
- Title (required)
- Description (required)
- URL link (optional, e.g. for more information)
- Image upload (JPEG/PNG, max 2MB)
- Activity type (select from list)
- Category (select from list)
- Tags (separated by commas; new tags are added automatically)
- Location info:
 - Address (displayed as text)
 - Latitude
 - Longitude
  
**Activity Types – 5 options**
- Activity
- Event
- Hobby opportunity
- Club
- Competition

**Categories – 10 options**
- Sports and exercise
- Music and performing arts
- Crafts and arts
- Science and technology
- Games and eSports
- Food and cooking
- Nature and outdoor activities
- Culture and history
- Community and volunteering
- Children and families

**Tags – 10 options**
*(If a tag doesn't exist, it will be automatically added.)*
- Free of charge
- Open to everyone
- Beginner-friendly
- Ongoing event
- Online
- Suitable for families
- Suitable for seniors
- Suitable for special groups
- Equipment available on-site
- Requires pre-registration

#### Two-Step Deletion
1.	Move to Trash (soft delete)
- The post is moved to the trash bin and is no longer visible as active.
- The user can restore the post or delete it permanently.
2.	Permanent Deletion
- The post is permanently deleted from the database and cannot be recovered.
- The user must confirm deletion separately to prevent mistakes:
"Are you sure you want to delete this post permanently? This action cannot be undone!"

### User Management (Admins only)
There are two roles in the admin panel:
1.	Regular Users (e.g. sports clubs or businesses)
a.	Can only view and manage their announcements.
2.	Administrators (Hobbly staff)
a.	Can manage all users and all announcements.
b.	Can create, edit, and delete user accounts.
c.	Can see all user information and their announcements.

## Assessment

The project will be assessed using Google Chrome and Firefox.
The axe browser extension is installed in Google Chrome and allows competitors to validate the website according to the accessibility standards WCAG.

## Mark distribution

| Description                     | Points |
| ------------------------------- | ------ |
| Registration                    | 10     |
| Login                           | 1      |
| Password Change                 | 2      |
| Managing Activity Announcements | 8      |
| User Management                 | 4,5    |
| Code quality                    | 3      |
| Project management              | 1,5    |
|                                 |        |
| **Total**                       | 30     |
