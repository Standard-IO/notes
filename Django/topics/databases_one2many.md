# One to many relation

- [One to many relation](#one-to-many-relation)
  - [how to use it?](#how-to-use-it)

Through this part we will se how to build a model of one to many ralation.

Every `models.Model` subclass is a table in database. Sometimes is necessary to make relations between tables this done with:

* Using `models.ForeignKey` class. This class require to assing another table and what happens with this column record is the foreing key is erased. This is done with `on_delete` argument for example if we want this column record exits after the foreign record is deleted we set this argumento to `models.SET_NULL`. In other way like we want to erase a record (éntry) from a table based on the erased content of another table set the argument to `models.CASCADE`.
   

```python
from django.db import models

# Create your models here.

class Artist(models.Model):
    name = models.CharField(max_length=200, db_index=True, help_text='Artist name')

    def __str__(self):
        """String for representing the Model object."""
        return self.name

class Album(models.Model):
    title = models.CharField(max_length=200, db_index=True, help_text='Album title')
    artist = models.ForeignKey('Artist', on_delete=models.SET_NULL, null=True)

    def __str__(self):
        """String for representing the Model object."""
        return self.title

class Genre(models.Model):
    name = models.CharField(max_length=200, db_index=True, help_text='Genre of music (i.e. Blues)')

    def __str__(self):
        """String for representing the Model object."""
        return self.name

class Track(models.Model):
    title = models.CharField(max_length=200, db_index=True, help_text='Track title')
    rating = models.IntegerField(null=True)
    length = models.IntegerField(null=True)
    count = models.IntegerField(null=True)
    album = models.ForeignKey('Album', on_delete=models.CASCADE)
    genre = models.ForeignKey('Genre', on_delete=models.SET_NULL, null=True)

    def __str__(self):
        """String for representing the Model object."""
        return self.title


```

## how to use it? 

To use the model is necessary to instanciate the class to create an object. We can make an example of this in the shell

```python
from trackmodel.models import Artist, Genre, Album, Track

# making an artist object
zep = Artist(name='Led Zeppeling')
zep.save() # saving

# making an album (this album needs a Artist object)
zep_iv = Album(title="IV", artist=zep)
zep_iv.save()

print(zep_iv.object.values()) # to see the values

# Genre
ROCK = Genre(name='ROCK')
ROCK.save()

# track
x = Track(title="about rock", rating=5, length=297, album=zip_iv, genre=ROCK)
x.save()

print(Track.objects.values())

# we can get items by primary key by
first = Track.objects.values(pk=1) # pk = "primarey key"

# we can acces to attibutes by dot puntuation
print(first.genre.name) # -> print ROCK


```