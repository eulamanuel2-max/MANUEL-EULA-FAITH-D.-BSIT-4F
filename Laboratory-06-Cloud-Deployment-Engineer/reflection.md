# Mission Reflection

> **Draft scaffold – write this in your own words (250–350 words).** The talking points below cover the technical parts; the personal parts (questions 4 and 5) must come from your own experience. Delete this note and the hints when you are done, and disclose any AI help if your instructor requires it.

## 1. How does writing a docker-compose.yml file make a cloud engineer's job easier than typing commands manually?

*Talking points:* one file describes the whole stack; one command to deploy (`up -d`) and one to remove (`down`); repeatable; can be saved in GitHub; fewer typing errors than long `docker run` commands with many flags.

[Your answer here]

## 2. What happens if you make an indentation error (like using a Tab instead of Spaces) in a YAML file?

*Talking points:* YAML uses spaces to show structure and does not allow tabs for indentation; Compose will fail with a parsing/syntax error and the stack will not start until it is fixed; wrong indentation can also move a key under the wrong parent.

[Your answer here]

## 3. Why did we use environment variables (like MYSQL_PASSWORD) in the Compose file?

*Talking points:* the same image can be configured without rebuilding it; the database container creates the user, database, and password from them, and the Nextcloud container uses the same values to connect; keeps configuration separate from the image; secrets should not be hard-coded in real deployments.

[Your answer here]

## 4. How did it feel to deploy a fully functional enterprise cloud storage system (Nextcloud) in just a few minutes?

*Your own experience:* What did you expect before running `docker-compose up -d`? What did you think when the Nextcloud setup page appeared in your browser?

[Your answer here]

## 5. How has your understanding of Cloud Computing evolved since Mission 1?

*Your own experience:* Compare where you started (Laboratory 01) with now. Which mission changed your view the most, and what do you understand differently about containers, storage, or Infrastructure as Code?

[Your answer here]
