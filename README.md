# Laravel Code Challenge I

## About

This document is designed to test an examinee's knowledge of PHP design principles and its implementations on Laravel framework.

### System
This project is about an image uploading system. User will sign-in and upload images.

### Development
The project will be done in 3 versions. First two of them are required to complete the project and the other one is optional.
You'll have 1 day to work on the project and decide how you're going to balance the things we care about (see below). Some people decide to do the required levels but keep the code clean and high quality as possible, and some care about the task completion.

We care about:
- Code Quality & Standartization
- Optimization
- Security
- Level Progress
- Deadline

Note that:
- Everything is API-based. No need to write a single HTML/CSS/JS code.
- The instructions below are not necceserly complete nor explicit; You can use your own ideas too.


### Output
You'll need to have your final code pushed into your own GitHub repository. 

## Version 1

We need a Laravel application to let users sign-up and sign-in in order to allow them to upload images.

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
1. Add an endpoint (`POST /api/files`) where user can upload a file with its title. Store the file in the local filesystem and save its path and title into the database.
1. Protect the endpoint from unauthorized access.

## Version 2

Now, we've decided to add another storage platform - S3. We need to configurate the app and use either local filesystem or the S3 instance.

### Intention
- Getting familiar with your coding quality and standardization ideas.

### Goals
- [ ] Implement a Strategy Pattern for uploading files to local filesystem and S3 platform

##### Instructions
1. Create two drivers called `FilesystemUploader` and `S3Uploader`
> Hint: It's OK to use mocked S3 uploads. We don't want its real functionality for this testing project.
1. Create a service called `FileUploader` 
1. Decide to use a driver by lookping up a `UPLOADER_DRIVER` environment variable as config.
> Hint: Write a new migration for `files` table and keep the strategy method used there.

## Version 3 (Optional)

Due to high usage of our AA (Awesome Application!), we're getting huge amount of image uploads. We need to cleanup old images periodicly - but also optimize how we perform table scans during its process.

### Intention
- Getting familiar with your researching process

### Goals
- [ ] Schedule a task to cleanup old files.
- [ ] Consider optimizing database for finding old records efficiently.

##### Instructions
1. Create a command called `files:cleanup` and remove files older than 3 days
> Note: Command may take long time. We don't need to have two instances of the scheduled command running at the same time.
1. Use [Laravel Scheduling](https://laravel.com/docs/9.x/scheduling) mechanism to schedule command every 20 seconds.
1. Research about how you can optimize `files` table to efficiently perform table scans during your SELECT query. Consider that the table will have near 1,000,000,000 records!
