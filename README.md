# Laravel Code Challenge I

## About

This document tests an examinee's knowledge of PHP design principles and its implementations on the Laravel framework.

### System
This project is about an image uploading system. The user will sign in and upload images.

### Development
The developer will do the project in 3 versions. The first two are required to complete the project, and the other is optional.
You'll have one day to work on the project and decide how you're going to balance the things we care about (see below). Some people choose to do the required levels but keep the code as clean and high quality as possible, and some care about the task completion.

We care about:
- Code Quality & Standardization
- Optimization
- Security
- Level Progress
- Deadline

Note that:
- Everything is API-based. No need to write a single HTML/CSS/JS code.
- The instructions below are not necessarily complete nor explicit; You can use your ideas too.


### Output
You'll need to have your final code pushed into your own GitHub repository. 

## Version 1

We need a Laravel application to let users sign up and sign in to allow them to upload images.

### Intention
- Knowing your familiarity with Laravel core features.
- Getting familiar with how you use git.

### Goals
- [ ] Implement sign-up and sign-in features using Laravel Sanctum
- [ ] Implement an endpoint to upload a new file

### Prerequisites
Use the following tables for your migrations:

```mysql
mysql> show columns from `users`;
+-------------------+-----------------+------+-----+---------+----------------+
| Field             | Type            | Null | Key | Default | Extra          |
+-------------------+-----------------+------+-----+---------+----------------+
| id                | bigint unsigned | NO   | PRI | NULL    | auto_increment |
| firstname         | varchar(255)    | NO   |     | NULL    |                |
| lastname          | varchar(255)    | NO   |     | NULL    |                |
| email             | varchar(255)    | NO   | UNI | NULL    |                |
| password          | varchar(255)    | NO   |     | NULL    |                |
| created_at        | timestamp       | NO   |     | NULL    |                |
| updated_at        | timestamp       | YES  |     | NULL    |                |
+-------------------+-----------------+------+-----+---------+----------------+
```

```mysql
mysql> show columns from `files`;
+-------------------+-----------------+------+-----+---------+----------------+
| Field             | Type            | Null | Key | Default | Extra          |
+-------------------+-----------------+------+-----+---------+----------------+
| id                | bigint unsigned | NO   | PRI | NULL    | auto_increment |
| user_id           | bigint unsigned | NO   | FRI | NULL    |                |
| path              | varchar(255)    | NO   | UNI | NULL    |                |
| title             | varchar(255)    | NO   | UNI | NULL    |                |
| created_at        | timestamp       | NO   |     | NULL    |                |
| updated_at        | timestamp       | YES  |     | NULL    |                |
+-------------------+-----------------+------+-----+---------+----------------+
```

##### Instructions
1. Create a Laravel project
1. Use [Laravel Sanctum](https://laravel.com/docs/9.x/sanctum) to implement [SPA](https://laravel.com/docs/9.x/sanctum#spa-authentication) sign-up and sign-in features.
1. Add an endpoint (`POST /api/files`) where the user can upload a file with its title. Store the file in the local filesystem and save its path and title into the database.
1. Protect the endpoint from unauthorized access.

## Version 2

Now, we've decided to add another storage platform - S3. We need to configure the app and use either the local filesystem or the S3 instance.

### Intention
- Getting familiar with your coding quality and standardization ideas.

### Goals
- [ ] Implement a Strategy Pattern for uploading files to the local filesystem and S3 platform

##### Instructions
1. Create two drivers called `FilesystemUploader` and `S3Uploader`
> Hint: It's OK to use mocked S3 uploads. We don't want its real functionality for this testing project.
1. Create a service called `FileUploader` 
1. Decide to use a driver by looking up a `UPLOADER_DRIVER` environment variable as config.
> Hint: Write a new migration for `files` table and keep the strategy method used there.

## Version 3 (Optional)

Due to the high usage of our AA (Awesome Application!), we're getting substantial image uploads! We need to clean up old images periodically and optimize how we perform table scans during its process.

### Intention
- Getting familiar with your research process

### Goals
- [ ] Schedule a task to clean up old files.
- [ ] Consider optimizing the database for finding old records efficiently.

##### Instructions
1. Create a command called `files:cleanup` and remove files older than 3 days
> Note: Command may take a long time. We don't need two instances of the scheduled command running simultaneously.
1. Use the [Laravel Scheduling](https://laravel.com/docs/9.x/scheduling) mechanism to schedule a command every 20 seconds.
1. Research how to efficiently optimize the `files` table to perform table scans during your SELECT query of the cleanup task. Consider that the table will have nearly 1,000,000,000 records!
