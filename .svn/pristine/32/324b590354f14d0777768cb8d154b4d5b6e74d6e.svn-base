#coding:utf-8
from django.db import models
from django.core.urlresolvers import reverse

# Create your models here.
class Publisher(models.Model):
    name = models.CharField(max_length=30)
    address = models.CharField(max_length=50)
    city = models.CharField(max_length=60)
    state_province = models.CharField(max_length=30)
    country = models.CharField(max_length=50)
    website = models.URLField()

    class Meta:
        ordering = ["-name"]

    def __unicode__(self):              # __unicode__ on Python 2
        return self.name

class Author(models.Model):
    salutation = models.CharField(max_length=10)
    name = models.CharField(max_length=200)
    email = models.EmailField()
    headshot = models.ImageField(upload_to='author_headshots', blank=True)

    def __unicode__(self):              # __unicode__ on Python 2
        return self.name
    """
    get_absolute_url()
    
    You don't even need to provide a success_url for CreateView or UpdateView
    they will use get_absolute_url() on the model object if available.
    PS.使用CreateView或者UpdateView如果成功则直接跳到models里面get_absolute_url()，而不用在views里提供
    success_url或者get_success_url()
    """
    def get_absolute_url(self):
        return reverse('author-detail', kwargs={'pk': self.pk})

class Book(models.Model):
    title = models.CharField(max_length=100)
    authors = models.ManyToManyField('Author')
    publisher = models.ForeignKey(Publisher)
    publication_date = models.DateField()
    
    def __unicode__(self):
        return "{0} - {1}".format(self.title, self.publication_date)