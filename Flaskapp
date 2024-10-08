from flask import Flask, render_template, request, redirect, url_for, session

app = Flask(__name__)
app.secret_key = 'your_secret_key'

# A simple in-memory storage for user data (for demonstration purposes)
users = {}

@app.route('/')
def home():
    return render_template('register.html')

@app.route('/register', methods=['POST'])
def register():
    username = request.form['username']
    password = request.form['password']
    firstname = request.form['firstname']
    lastname = request.form['lastname']
    email = request.form['email']
    
    # Store user data
    users[username] = {
        'password': password,
        'firstname': firstname,
        'lastname': lastname,
        'email': email
    }
    
    return redirect(url_for('info'))

@app.route('/info')
def info():
    return render_template('info.html', users=users)

@app.route('/login', methods=['POST'])
def login():
    username = request.form['username']
    password = request.form['password']

    if username in users and users[username]['password'] == password:
        session['username'] = username
        return redirect(url_for('user_info'))
    else:
        return redirect(url_for('info'))

@app.route('/user_info')
def user_info():
    username = session.get('username')
    user_data = users.get(username, {})
    
    return render_template('user_info.html', user_data=user_data)

if __name__ == '__main__':
    app.run('0.0.0.0',port=80,debug=True)
