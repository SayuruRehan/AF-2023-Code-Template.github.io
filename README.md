# AF-2023-Code-Template

## Question 01 - Theory-based (10 Marks)

## Question 02 - Express JS (20 Marks)

1. Setup an express JS project.

2. Use the JSON middleware.

3. Install Mongoose.
```
npm install mongoose
```

4. Implement the following.
```
const express = require('express');
const mongoose = require('mongoose');

const app = express();
const port = 3000;

app.use(express.json());

mongoose.connect('mongodb://localhost:27017/university', {
 useNewUrlParser: true,
 useUnifiedTopology: true
});
```

5. Implement the db object as follows.
```
const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
 console.log('Connected to MongoDB database');
});

6. Implement the student schema as follows.
const studentSchema = new mongoose.Schema({
 name: String,
 studentId: String
});
```

7. Implement the Student model as follows
```
const Student = mongoose.model('Student', studentSchema);
```

8. Implement the get method for request all students.
```
// Get all Students
app.get('/api/Students', async (req, res) => {
 const students = await Student.find();
 res.status(200).json(students);
});
```

9. Implement the get method to request only one student.
```
// Get a single student
app.get('/api/students/:id', async (req, res) => {
 const student = await Student.findById(req.params.id);
 res.status(200).json(student);
});
```

10. Implement the post method to create a new student entry.
```
// Create a new student
app.post('/api/students', async (req, res) => {
 const student = new Student({
  name: req.body.name,
  studentId: req.body.studentId
 });
 await student.save();
 res.status(201).json(student);
});
```

11. Implement the put method to update an existing student.
```
// Update a student
app.put('/api/students/:id', async (req, res) => {
 const student = await Student.findByIdAndUpdate(req.params.id, {
  name: req.body.name,
  studentId: req.body.studentId
 }, { new: true });
 res.status(200).json(student);
});
```

12. Implement the delete method to delete a student.
```
// Delete a student
app.delete('/api/students/:id', async (req, res) => {
 await Student.findByIdAndDelete(req.params.id);
 res.status(204).json({ message: 'Student deleted' });
});
```

13. Let’s run the app and test everything.
```
app.listen(port, () => {
 console.log(`Server listening on port ${port}`);
});
```

14. Use postman to test the APIs.

15. Use MongoDB Compass to see the database.

16. Modify the code by introducing middleware to validate the requests.


## Question 03 - Spring Boot (20 Marks)

## Question 04 - Practical based REST API (25 Marks)

- Create a new directory for your new Express.js project and run the following command inside that folder
```
npm install express body-parser –save
```
- This will install Express.js and Body Parser, which we will use to parse incoming requests.
<br/>
- Then create a new file called, <b>index.js</b> and add the following code:
```
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

let todos = [
 { id: 1, text: 'Buy groceries', done: false },
 { id: 2, text: 'Do laundry', done: true },
];

app.get('/api/todos', (req, res) => {
 res.send(todos);
});

app.get('/api/todos/:id', (req, res) => {
 const id = Number(req.params.id);
 const todo = todos.find(todo => todo.id === id);
 if (todo) {
   res.send(todo);
 } else {
   res.status(404).send('Todo not found');
 }
});

app.post('/api/todos', (req, res) => {
 const { text, done } = req.body;
 const id = todos.length + 1;
 const todo = { id, text, done };
 todos.push(todo);
 res.send(todo);
});

app.put('/api/todos/:id', (req, res) => {
 const id = Number(req.params.id);
 const { text, done } = req.body;
 const todo = todos.find(todo => todo.id === id);
 if (todo) {
   todo.text = text || todo.text;
   todo.done = done || todo.done;
   res.send(todo);
 } else {
   res.status(404).send('Todo not found');
 }
});

app.delete('/api/todos/:id', (req, res) => {
 const id = Number(req.params.id);
 todos = todos.filter(todo => todo.id !== id);
 res.send(`Todo with id ${id} has been deleted`);
});

app.listen(port, () => {
 console.log(`Example app listening at http://localhost:${port}`);
});
```

- Finally, run the file with the node command.
```
node index.js
```

## Question 05 - Frontend Development (25 Marks)

- Create a simple “Hello World” app that displays a greeting message to the user.
    - Start by creating a new React component called “Greeting”.
    - Inside the “Greeting” component, return a JSX element that displays a greeting message to the user, such as “Hello World!”.
    - Render the “Greeting” component in your main app component

```
import React from 'react';

// Step 1: Create a new React component called "Greeting"
const Greeting = () => {
  // Step 2: Return a JSX element that displays a greeting message
  return <h1>Hello World!</h1>;
};

// Step 3: Render the "Greeting" component in your main app component
const App = () => {
  return (
    <div>
      <Greeting />
    </div>
  );
};

export default App;
```

- In this example, we have a functional component called Greeting that returns a JSX element "Hello World!", which represents the greeting message. Then, in the App component, we render the Greeting component, encapsulated in a div element.

- To run this app, you’ll need to set up a React development environment, including installing Node.js and creating a new React project using a tool like Create React App. Once the project is set up, replace the content of the App.js file with the code provided and start the development server.

- When you open the app in your browser, you should see the greeting “Hello World!” displayed on the screen.

### Create a “NavBar” component that displays a navigation menu.
- Start by creating a new React component called “NavBar”.
- Inside the “NavBar” component, return a JSX element that displays a navigation menu. This can be a simple unordered list with a few links to different pages or sections of your app.
- Render the “NavBar” component in your main app component.

```
import React from 'react';

// Step 1: Create a new React component called "NavBar"
const NavBar = () => {
  // Step 2: Return a JSX element that displays a navigation menu
  return (
    <nav>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
    </nav>
  );
};

// Step 3: Render the "NavBar" component in your main app component
const App = () => {
  return (
    <div>
      <NavBar />
      {/* Your other app content goes here */}
    </div>
  );
};

export default App;
```

- In this example, we have a functional component called NavBar that returns a JSX element representing a navigation menu. The navigation menu is structured as an unordered list with several list items, each containing an anchor tag representing a link to a different page or section of the app. You can modify the href attribute of the anchor tags to point to the appropriate URLs in your application.

- In the App component, we render the NavBar component, followed by your other app content. The NavBar component will be displayed at the top of the app, and you can place the rest of your app’s content below it.

- Remember to set up your React development environment and replace the content of the App.js file with the code provided.

### OR

NavBar.js:

```
  import React from 'react';

    const NavBar = () => {
      return (
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/about">About</a></li>
            <li><a href="/contact">Contact</a></li>
          </ul>
        </nav>
      );
    };

  export default NavBar;
```

Home.js:
```
  import React from 'react';
  
  const Home = () => {
    return <h1>Welcome to the Home Page!</h1>;
  };
  
  export default Home;
```

About.js:
```
  import React from 'react';
  
  const About = () => {
    return <h1>About Us</h1>;
  };
  
  export default About;
```

Contact.js:
```
  import React from 'react';
  
  const Contact = () => {
    return <h1>Contact Us</h1>;
  };
  
  export default Contact;
```

App.js:
```
  import React from 'react';
  import NavBar from './NavBar';
  import Home from './Home';
  import About from './About';
  import Contact from './Contact';
  
  const App = () => {
    return (
      <div>
        <NavBar />
        <Home />
        {/* Your other app content goes here */}
        <About />
        <Contact />
      </div>
    );
  };
  
  export default App;
```

- In this updated example, each page component (Home, About, Contact) is created in separate files and imported into the App.js file. The NavBar component is also created in a separate file and imported.

- Ensure that all the component files are in the same directory as the App.js file or adjust the import paths accordingly if they are in different directories.

- By organizing your code into separate files, it becomes easier to manage and maintain your React application.

<br/>
<b>Create a “Footer” component that displays a copyright message and links to your social media profiles.<br/>
Create a “Card” component that displays an image, title, and description for a product or service.<br/>
Create a “Button” component that displays a customizable button with different styles and sizes.<br/>
Create a “Banner” component that displays a promotional message or call-to-action with a background image or colour.<br/>
Create a “Testimonial” component that displays a quote, name, and photo for a customer testimonial or review<br/></b>
<br/>
<br/>
Footer.js:
```
import React from 'react';

const Footer = () => {
  return (
    <footer>
      <p>&copy; 2023 Your Website. All rights reserved.</p>
      <div>
        <a href="https://example.com">Facebook</a>
        <a href="https://example.com">Twitter</a>
        <a href="https://example.com">Instagram</a>
      </div>
    </footer>
  );
};

export default Footer;
```

Card.js:
```
import React from 'react';

const Card = ({ imageSrc, title, description }) => {
  return (
    <div className="card">
      <img src={imageSrc} alt={title} />
      <h2>{title}</h2>
      <p>{description}</p>
    </div>
  );
};

export default Card;
```

Button.js:
```
import React from 'react';

const Button = ({ text, style, size }) => {
  const classNames = `button ${style} ${size}`;

  return <button className={classNames}>{text}</button>;
};

export default Button;
```

Banner.js:
```
import React from 'react';

const Banner = ({ message, background }) => {
  const bannerStyle = {
    background: background,
  };

  return (
    <div className="banner" style={bannerStyle}>
      <p>{message}</p>
    </div>
  );
};

export default Banner;
```

Testimonial.js:
```
import React from 'react';

const Testimonial = ({ quote, name, photo }) => {
  return (
    <div className="testimonial">
      <blockquote>{quote}</blockquote>
      <p className="name">{name}</p>
      <img src={photo} alt={name} />
    </div>
  );
};

export default Testimonial;
```

App.js:
```
import React from 'react';
import NavBar from './NavBar';
import Footer from './Footer';
import Home from './Home';
import About from './About';
import Contact from './Contact';
import Card from './Card';
import Button from './Button';
import Banner from './Banner';
import Testimonial from './Testimonial';

const App = () => {
  return (
    <div>
      <NavBar />
      <Home />
      {/* Your other app content goes here */}
      <About />
      <Contact />

      <Card
        imageSrc="product.jpg"
        title="Product Title"
        description="Product Description"
      />

      <Button text="Click Me" style="primary" size="small" />

      <Banner message="Special Offer!" background="#f2f2f2" />

      <Testimonial
        quote="This product changed my life!"
        name="John Doe"
        photo="testimonial.jpg"
      />

      <Footer />
    </div>
  );
};

export default App;
```

All the best! ❤️
