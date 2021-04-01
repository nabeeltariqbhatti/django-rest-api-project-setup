# django-rest-api-project-setup

django-rest-api-project-setup


using Documentation

[Documentation Link](https://www.django-rest-framework.org/#installation)



[](https://www.django-rest-framework.org/img/logo.png)



Django REST framework is a powerful and flexible toolkit for building Web APIs.

Some reasons you might want to use REST framework:

The Web browsable API is a huge usability win for your developers.

Authentication policies including packages for OAuth1a and OAuth2.

Serialization that supports both ORM and non-ORM data sources.

Customizable all the way down - just use regular function-based views if you don't need the more powerful features.
Extensive documentation, and great community support.<br/>

Used and trusted by internationally recognised companies including Mozilla, Red Hat, Heroku, and Eventbrite.


Requirements
REST framework requires the following:

Python (3.5, 3.6, 3.7, 3.8, 3.9)
Django (2.2, 3.0, 3.1)
We highly recommend and only officially support the latest patch release of each Python and Django series.

The following packages are optional:

PyYAML, uritemplate (5.1+, 3.0.0+) - Schema generation support.
Markdown (3.0.0+) - Markdown support for the browsable API.
Pygments (2.4.0+) - Add syntax highlighting to Markdown processing.
django-filter (1.0.1+) - Filtering support.
django-guardian (1.1.1+) - Object level permissions support.
Installation
Install using pip, including any optional packages you want...

pip install djangorestframework
pip install markdown       # Markdown support for the browsable API.
pip install django-filter  # Filtering support
...or clone the project from github.

git clone https://github.com/encode/django-rest-framework
Add 'rest_framework' to your INSTALLED_APPS setting.

INSTALLED_APPS = [
    ...
    'rest_framework',
]
If you're intending to use the browsable API you'll probably also want to add REST framework's login and logout views. Add the following to your root urls.py file.

urlpatterns = [<br/>
    ...
    path('api-auth/', include('rest_framework.urls'))<br/>
]<br/>
Note that the URL path can be whatever you want.<br/>

Example<br/>
Let's take a look at a quick example of using REST framework to build a simple model-backed API.<br/>

We'll create a read-write API for accessing information on the users of our project.<br/>

Any global settings for a REST framework API are kept in a single configuration dictionary named REST_FRAMEWORK. Start off by adding the following to your settings.py module:<br/>

REST_FRAMEWORK = {<br/>
    # Use Django's standard `django.contrib.auth` permissions,<br/>
    # or allow read-only access for unauthenticated users.<br/>
    'DEFAULT_PERMISSION_CLASSES': [<br/>
        'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'<br/>
    ]<br/>
}<br/>
Don't forget to make sure you've also added rest_framework to your INSTALLED_APPS.<br/>

We're ready to create our API now. Here's our project's root urls.py module:<br/>

from django.urls import path, include<br/>
from django.contrib.auth.models import User<br/>
from rest_framework import routers, serializers, viewsets<br/>

# Serializers define the API representation.<br/>
class UserSerializer(serializers.HyperlinkedModelSerializer):<br/>
    class Meta:<br/>
        model = User<br/>
        fields = ['url', 'username', 'email', 'is_staff']<br/>

# ViewSets define the view behavior.<br/>
class UserViewSet(viewsets.ModelViewSet):<br/>
    queryset = User.objects.all()<br/>
    serializer_class = UserSerializer<br/>

# Routers provide an easy way of automatically determining the URL conf.<br/>
router = routers.DefaultRouter()<br/>
router.register(r'users', UserViewSet)<br/>

# Wire up our API using automatic URL routing.<br/>
# Additionally, we include login URLs for the browsable API.<br/>
urlpatterns = [<br/>
    path('', include(router.urls)),<br/><br/>
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))<br/>
]<br/>
You can now open the API in your browser at http://127.0.0.1:8000/, and view your new 'users' API. If you use the login control in the top right corner you'll also be able to add, create and delete users from the system.

Quickstart<br/>
Can't wait to get started? The quickstart guide is the fastest way to get up and running, and building APIs with REST framework.<br/>

Development<br/>
See the Contribution guidelines for information on how to clone the repository, run the test suite and contribute changes back to REST Framework.<br/>

Support
For support please see the REST framework discussion group, try the #restframework channel on irc.freenode.net, search the IRC archives, or raise a question on Stack Overflow, making sure to include the 'django-rest-framework' tag.<br/>

For priority support please sign up for a professional or premium sponsorship plan.<br/><br/>

Security<br/>
If you believe you’ve found something in Django REST framework which has security implications, please do not raise the issue in a public forum.<br/>

Send a description of the issue via email to rest-framework-security@googlegroups.com. The project maintainers will then work with you to resolve any issues where required, prior to any public disclosure.
<br/>
License
Copyright © 2011-present, Encode OSS Ltd. All rights reserved.<br/>

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:<br/>

Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.<br/>

Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
<br/>
Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
<br/>

