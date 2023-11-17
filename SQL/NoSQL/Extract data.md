# Exploiting syntax injection to extract data

In many NoSQL databases, some query operators or functions can run limited JavaScript code, such as MongoDB's $where operator and mapReduce() function. This means that, if a vulnerable application uses these operators or functions, the database may evaluate the JavaScript as part of the query. You may therefore be able to use JavaScript functions to extract data from the database.
