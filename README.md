- 👋 Hi, I’m @umeshnayak-log
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
umeshnayak-log/umeshnayak-log is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
from flask import *
import sqlite3

app=Flask(__name__)
connect=sqlite3.connect("database.db")
connect.execute("CREATE TABLE IF NOT EXISTS DETAILS(name TEXT,email TEXT)")
connect.execute('CREATE TABLE IF NOT EXISTS bookingdata(name TEXT,email TEXT,phone TEXT,address TEXT,city TEXT,adults TEXT,requests TEXT,date TEXT )')
@app.route("/", methods=["GET","POST"])
def home():
        if request.method=="POST":
                name=request.form["name"]
                email=request.form["email"]
                name=request.form["password"]
                email=request.form["password"]

                with sqlite3.connect("database.db") as users:
                        cursor=users.cursor()
                        cursor.execute("INSERT INTO DETAILS (name, email) VALUES (?,?)", (name, email))
                        users.commit()
                return render_template("registration.html")
        else:
                return render_template("home.html")

@app.route("/registration", methods=["GET","POST"])
def registration():
        if request.method=="POST":
                return render_template("registration.html")
        else:
                return render_template("home.html")
@app.route('/data')
def data():
	with sqlite3.connect('database.db')as users:
		cursor=users.cursor()
		cursor.execute('SELECT * FROM DETAILS')
		data=cursor.fetchall()
		return render_template('data.html',data=data)
@app.route('/delete/<id>')
def delete(id):
	with sqlite3.connect('database.db')as users:
		cursor=users.cursor()
		cursor.execute(f'DELETE FROM bookingdata WHERE email="{id}";')		
		return render_template('registration.html',data=data)
@app.route('/edit',methods=('GET','POST'))
def edit():
        if request.method=='POST':
                name=request.form['name']
                email=request.form['email']
                phone=request.form['phone']
                address=request.form['address']
                city=request.form['city']
                adults=request.form['adults']
                requests=request.form['requests']
                date=request.form['date']
                data=[name, email,phone,address,city,adults,requests,date]
                return render_template('edit.html',data=data)
@app.route('/edited_data',methods=('GET','POST'))
def edited_data():
	if request.method=='POST':
                name=request.form['name']
                email=request.form['email']
                phone=request.form['phone']
                address=request.form['address']
                city=request.form['city']
                adults=request.form['adults']
                requests=request.form['requests']
                date=request.form['date']
                with sqlite3.connect('database.db')as users:
                        cursor=users.cursor()
                        cursor.execute(f'UPDATE bookingdata SET name="{name}",email="{email}",phone="{phone}",address="{address}",city="{city}",adults="{adults}",requests="{requests}",date="{date}" where email="{email}";')
                        return redirect('/bookingdata')

@app.route('/bookingdata')
def bookingdata():
	with sqlite3.connect('database.db')as users:
		cursor=users.cursor()
		cursor.execute('SELECT * FROM bookingdata')
		data=cursor.fetchall()
		return render_template('bookingdata.html',data=data)
@app.route("/about", methods=["GET","POST"])
def about():
        if request.method=="POST":
                return render_template("home.html")
        else:
                return render_template("about.docx")

@app.route("/booking", methods=["GET","POST"])
def booking():
        if request.method=="POST":
                name=request.form['name']
                email=request.form['email']
                phone=request.form['phone']
                address=request.form['address']
                city=request.form['city']
                adults=request.form['adults']
                requests=request.form['requests']
                date=request.form['date']
                with sqlite3.connect("database.db") as users:
                        cursor=users.cursor()
                        cursor.execute("INSERT INTO bookingdata(name, email,phone,address,city,adults,requests,date) VALUES (?,?,?,?,?,?,?,?)", (name, email,phone,address,city,adults,requests,date))
                        users.commit()
                        return render_template("registration.html")
        else:
                return render_template("booking.html")


@app.route("/contact", methods=["GET","POST"])
def contact():
        if request.method=="POST":
                return render_template("home.html")
        else:
                return render_template("contact.html")

@app.route("/parks", methods=["GET","POST"])
def parks():
        if request.method=="POST":
                return render_template("home.html")
        else:
                return render_template("parks.html")
@app.route("/temples", methods=["GET","POST"])
def temples():
	if request.method=="POST":
		return render_template("home.html")
	else:
		return render_template("temples.html")
@app.route("/beaches", methods=["GET","POST"])
def beaches():
	if request.method=="POST":
		return render_template("home.html")
	else:
		return render_template("beaches.html")
@app.route("/historicalplaces", methods=["GET","POST"])
def historicalplaces():
	if request.method=="POST":
		return render_template("home.html")
	else:
		return render_template("historicalplaces.html")
@app.route("/famouscities", methods=["GET","POST"])
def famouscities():
	if request.method=="POST":
		return render_template("home.html")
	else:
		return render_template("famouscities.html")
@app.route("/famousplaces", methods=["GET","POST"])
def famousplaces():
	if request.method=="POST":
		return render_template("home.html")
	else:
		return render_template("famousplaces.html")


if __name__=="__main__":
	app.run(debug="True")
   
