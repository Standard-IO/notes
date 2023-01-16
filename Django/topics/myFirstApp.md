# My first app in Django. All need your to know (html, css, etc)

## Installation of the Django and git repository for course

In the next section we will use the page provided by the course to follow the instructions in how to install and get the repostories to work with Django and understand how it works.

[https://www.dj4e.com/assn/dj4e_install.md](https://www.dj4e.com/assn/dj4e_install.md)

To manage the project requeriments files in a Poetry we could use this code:

```bash
cat requirements.txt | grep -E '^[^# ]' | cut -d= -f1 | xargs -n 1 poetry add
```

In the course is followed this introduction to Django provided by the Django docs: 

Tutorial: [my first app](https://docs.djangoproject.com/en/4.0/intro/tutorial01/#creating-the-polls-app)

This totial stablish how to enable for first time e projecto and implement your first app.

