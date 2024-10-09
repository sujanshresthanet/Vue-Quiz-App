Vue.js Quiz App
===============

A simple and interactive quiz application built with Vue.js that allows users to take quizzes, view their results, and track their performance.

Table of Contents
-----------------

1.  [Features](#features)
2.  [Installation](#installation)
3.  [Usage](#usage)
4.  [File Structure](#file-structure)
5.  [Contributing](#contributing)
6.  [License](#license)

Features
--------

*   50+ quiz questions with single-choice answers.
*   User-friendly interface with Bootstrap 5.
*   Displays score and summary at the end of the quiz.
*   Tracks correct and incorrect answers with percentage calculations.
*   Allows users to finish the quiz at any time and view their summary.
*   Option to restart the quiz.
*   Progress tracking using local storage to resume the quiz.

Installation
------------

1.  Ensure you have Node.js installed on your machine.
2.  Clone this repository to your local machine using the command:

    git clone https://github.com/sujanshresthanet/vue-quiz-app.git

4.  Navigate to the project directory:

    cd vue-quiz-app

6.  Install the required dependencies:

    npm install

Usage
-----

1.  Start the development server:

    npm run serve

3.  Open your web browser and go to [http://localhost:8080](http://localhost:8080).
4.  Take the quiz and follow the on-screen instructions.

File Structure
--------------

    
    vue-quiz-app/
    ├── public/
    │   ├── index.html
    │   └── favicon.ico
    ├── src/
    │   ├── assets/
    │   ├── components/
    │   │   └── QuizQuestion.vue
    │   ├── App.vue
    │   ├── main.js
    │   └── router.js (if using Vue Router)
    ├── package.json
    └── README.md
    

Contributing
------------

Contributions are welcome! If you'd like to contribute, please fork the repository and submit a pull request with your changes.

License
-------

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.