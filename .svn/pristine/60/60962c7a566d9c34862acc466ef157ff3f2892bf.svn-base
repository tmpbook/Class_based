from django.conf.urls import patterns, include, url
from books.views import PublisherList, BookList, PublisherBookList, AuthorDetailView, AuthorList
from books.views import AuthorCreate, AuthorUpdate, AuthorDelete

from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'Class_based.views.home', name='home'),
    # url(r'^blog/', include('blog.urls')),

    url(r'^admin/', include(admin.site.urls)),
    url(r'^publishers/$', PublisherList.as_view(), name='publisher-list'),
    url(r'^books/$', BookList.as_view(), name='book-list'),
    url(r'^books/([\w-]+)/$', PublisherBookList.as_view(), name='book-detail'),
    url(r'^authors/$', AuthorList.as_view(), name='author-list'),
    url(r'^authors/(?P<pk>\d+)/$', AuthorDetailView.as_view(), name='author-detail'),
    url(r'^author/add/$', AuthorCreate.as_view(), name='author-create'),
    url(r'^author/(?P<pk>\d+)/$', AuthorUpdate.as_view(), name='author-update'),    
    url(r'^author/(?P<pk>\d+)/delete/$', AuthorDelete.as_view(), name='author-delete'),
)
