# Laravel Code Challenge I

## About

This document is designed to test an examinee's knowledge of PHP design principles and its implementations on Laravel framework.

### System
This project is about a file uploading system. User can sign-in and upload files.

### Development
The project has been designed in 4 levels. First two of them are required to complete the project and two others are optional. The parameters we care are code quality, feature implementation and the deadline.
You'll have 1 day to work on the project and decide how you're going to balance those three mentioned parameters. Some people decinde to do the required levels but keep the code clean and high quality as possible, and some care about the task completion. Note that everything is API-based. No need to write a single HTML/CSS/JS code.

### Output
You'll need to have your final code pushed into your own GitHub repository. 

## Level 1

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

