# The admin User

Is necessary to have a admin user this user will control all the things in our application. This user lets to create another users in the project.

> Django comes with a user authentication system. It handles user accounts, groups, permissions and cookie-based user sessions.  The authentication system consists of:
> 
> Users
> Permissions: Binary (yes/no) flags designating whether a user may perform a certain task.
> Groups: A generic way of applying labels and permissions to more than one user.
> A configurable password hashing system
> Forms and view tools for logging in users, or restricting content
> A pluggable backend system
> 
> Authentication support is bundled as a Django contrib module in django.contrib.auth. By default, the required configuration is already included in settings.py.

[DJango Docs](https://docs.djangoproject.com/en/4.0/topics/auth/)

To create a super user is made with the next code, the mail is necessary to recover the password:

```
dj4e-samples$ python3 manage.py createsuperuser
Username: dj4e-samples
Email address: csev@umich.edu
Password: 
Password (again): 
Superuser created successfully.

```

## Wiping your database

Is normal to start for fresh database is you have one this can be done erasing the previous one.

Note: if you erase the database is necessary to create again the super user.

```
dj4e-samples$ rm db.sqlite3
dj4e-samples$ python3 manage.py migrate
dj4e-samples$ python3 manage.py createsuperuser
Username: *dj4e-samples
Email address: csev@umich.edu
Password: 
Password (again): 
Superuser created successfully.

```

## aditional database

* Once you have a super user you can log into your application and create additional new users, associate them with groups, and give them permissions in the "/admin" user interface
* Many applications don’t need to use the groups or permissions features of Django
 
