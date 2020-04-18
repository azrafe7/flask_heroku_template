## NOTES (Windows)

### LOCAL SETUP

 - be sure to have virtualenv installed (`pip install virtualenv`)
 - create folder <flask_app> (name is irrelevant)
 - enter it
 - run `virtualenv venv`
 - activate the virtual env by running `venv\Scripts\activate`
 - should now see `(venv)` beside your prompt
 - `pip install flask gunicorn jinja2`
 - create the file that will be the entry point of the flask app
    ```python
    #flask_app.py
    
    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_flask():
        return 'Hello Flask!'

    if __name__ == '__main__':
        app.run()
     ```
 - test it locally with `python flask_app.py`
 - should output something like
    ```
    * Serving Flask app "flask_app" (lazy loading)
    * Environment: production
      WARNING: This is a development server. Do not use it in a production deployment.
      Use a production WSGI server instead.
    * Debug mode: off
    * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    ```
 - going to that address should output `Hello Flask!`
 - quit the server (`CTRL+C`)
 - create a file named `Procfile` (no extension) with this content
    ```
    web: gunicorn flask_app:app
    ```
 - run `pip freeze > requirements.txt` to write a requirements file by listing the dependencies installed in the current virtual env
 - **IMPORTANT:** you should ensure that `requirements.txt` is encoded in ANSI for it to be deployed to Heroku successfully (but Heroku will work out anyway even if you skip this step)
 - now `requirements.txt` should contain something like
    ```
    click==7.1.1
    Flask==1.1.2
    gunicorn==20.0.4
    itsdangerous==1.1.0
    Jinja2==2.11.2
    MarkupSafe==1.1.1
    Werkzeug==1.0.1
    ```
 
 ### INIT GIT

 - create a `.gitignore` file with this contents
    ```
    # ignore virtualenv folder
    venv/
    ```
 - init git repo and make first commit by running in sequence
    ```
    git init
    git add .
    git commit -m "first commit: ready to deploy initial app"
    ```

### DEPLOY TO HEROKU

 - login to the Heroku Toolbelt running `heroku login`
 - create a remote Heroku app running `heroku create`
   (**NOTE:** this will assign a random name to the app; you can run `heroku create your-app-name` to give it a meaningful name. You can change the name later anyway)
 - should output something like
    ```
    Creating app... done, ⬢ boiling-fjord-61012
    https://boiling-fjord-61012.herokuapp.com/ | https://git.heroku.com/boiling-fjord-61012.git
    ```
 - deploy the app to Heroku with `git push heroku master`
 - should push the repo to the heroku servers and produce something like this in the shell
    ```
    Enumerating objects: 7, done.
    Counting objects: 100% (7/7), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (7/7), 1.28 KiB | 655.00 KiB/s, done.
    Total 7 (delta 0), reused 0 (delta 0)
    remote: Compressing source files... done.
    remote: Building source:
    remote:
    remote: -----> Python app detected
    remote: cp: cannot create regular file '/app/tmp/cache/.heroku/requirements.txt': No such file or directory
    remote: -----> Installing python-3.6.10
    remote: -----> Installing pip
    remote: -----> Installing SQLite3
    remote: Sqlite3 successfully installed.
    remote: -----> Installing requirements with pip
    remote:        Collecting click==7.1.1
    remote:          Downloading click-7.1.1-py2.py3-none-any.whl (82 kB)
    remote:        Collecting Flask==1.1.2
    remote:          Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
    remote:        Collecting gunicorn==20.0.4
    remote:          Downloading gunicorn-20.0.4-py2.py3-none-any.whl (77 kB)
    remote:        Collecting itsdangerous==1.1.0
    remote:          Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
    remote:        Collecting Jinja2==2.11.2
    remote:          Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
    remote:        Collecting MarkupSafe==1.1.1
    remote:          Downloading MarkupSafe-1.1.1-cp36-cp36m-manylinux1_x86_64.whl (27 kB)
    remote:        Collecting Werkzeug==1.0.1
    remote:          Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
    remote:        Installing collected packages: click, Werkzeug, MarkupSafe, Jinja2, itsdangerous, Flask, gunicorn
    remote:        Successfully installed Flask-1.1.2 Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.1 gunicorn-20.0.4 itsdangerous-1.1.0
    remote: -----> Discovering process types
    remote:        Procfile declares types -> web
    remote:
    remote: -----> Compressing...
    remote:        Done: 45.1M
    remote: -----> Launching...
    remote:        Released v3
    remote:        https://boiling-fjord-61012.herokuapp.com/ deployed to Heroku
    remote:
    remote: Verifying deploy... done.
    To https://git.heroku.com/boiling-fjord-61012.git
    * [new branch]      master -> master   
    ```
 - now you can try the app online going to `https://boiling-fjord-61012.herokuapp.com/ `



## CREDITS
http://www.gtlambert.com/blog/deploy-flask-app-to-heroku (George Lambert)
