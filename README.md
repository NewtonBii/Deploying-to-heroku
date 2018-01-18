# Deploying-to-heroku
## Steps to Deploy Django Apps on Heroku

  * Create a ``Procfile`` in the root folder and type ``web: gunicorn <name of your app>.wsgi``
  * Create ``requirements.txt`` in the root folder by ``pip freeze >requirements.txt``
  * Create a ``runtime.txt`` in the app root folder and type the python version your app is using for example ``python-3.6.3``
  * Setup the static assets by:
      * In your **settings.py**
      ``PROJECT_ROOT = os.path.dirname(os.path.abspath(__file__))

        # Static files (CSS, JavaScript, Images)
        * STATIC_ROOT = os.path.join(PROJECT_ROOT, 'staticfiles')
        * STATIC_URL = '/static/'

        # Extra places for collectstatic to find static files.
        STATICFILES_DIRS = (
            os.path.join(PROJECT_ROOT, 'static'),)
      ``
      * Install whitenoise ``python3.6 -m pip install whitenoise``
      * Add whitenoise to your **wsgi.py** file.
      ``import os
        from django.core.wsgi import get_wsgi_application
        from whitenoise.django import DjangoWhiteNoise

        os.environ.setdefault("DJANGO_SETTINGS_MODULE", "bootcamp.settings")

        application = get_wsgi_application()
        application = DjangoWhiteNoise(application)
      ``
      * Update **settings.py**
      ``STATICFILES_STORAGE = 'whitenoise.django.GzipManifestStaticFilesStorage'``

      * Deploy:
      ``git add .;git commit -m "Deploy to heroku";git push heroku master;heroku open``
