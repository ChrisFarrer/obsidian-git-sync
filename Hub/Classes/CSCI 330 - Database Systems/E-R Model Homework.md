---
Title: E-R Model Homework
Source: 
Date: 2023-12-03
Class: CSCI 305 - Analysis of Algorithms 1
---
# E-R Development Quiz

## Prompt

Suppose you are given the following requirements for a simple database for the Fédération Internationale de Football Association (FIFA):

- FIFA has many teams,
- Each team has a name, a city, a coach, a captain, and a set of players,
- Each player belongs to only one team,
- Each player has a name, a position (such as Full-Back or Winger), a skill level, and a set of injury records,
- A team captain is also a player,
- A game is played between two teams (referred to as host_team and guest_team) and has a time (such as 11:50 pm, May 11th, 2023) and a score (such as 3 to 1).

You will need to do the followings:

- Construct a clean and concise ER diagram for the FIFA database.
- Generate a schema by eliminating redundancy and normalizing your design
- Implement your design using SQL code. 

Note:

1. The positions of a football game (or a soccer game) can be found [hereLinks to an external site.](https://www.bundesliga.com/en/bundesliga/news/soccer-positions-explained-names-numbers-what-they-do-2579-786).
2. If you think more assumptions are required to facilitate the process, please list your assumptions in your diagram.
3. You can use any tools you prefer (e.g., drawing on paper and take a picture, LucidChart, draw.io, etc.)
4. Please submit one PDF file.


## E-R Diagram

Given the prompt, the following E-R Diagram could be implemented:
![[Drawing 2023-12-03 23.04.42.excalidraw.png]]

In this diagram, I used diamonds to indicate the relationships between tables, but rather than give them names, I explicitly stated the foreign keys used to connect them both using an asterisk and a side description. The functionality of the database was largely left to interpretation, so the diagram above could be refactored to fit different features. One of these would be splitting the "Games" table into "Game Scores" and "Game Schedule". This allows future games to be input into the database without having null values in the score attribute.

The E-R Diagram could be implemented into a MySQL schema using the following code:
```sql
-- Teams table
CREATE TABLE teams (
  team_name VARCHAR(255) NOT NULL UNIQUE,
  city VARCHAR(255) NOT NULL,
  coach VARCHAR(255) NOT NULL,
  captain VARCHAR(255) NOT NULL,
  FOREIGN KEY (captain) REFERENCES teams (player_id)
  PRIMARY KEY (team_name)
);

-- Players table
CREATE TABLE players (
  player_id INT NOT NULL AUTO_INCREMENT,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  position VARCHAR(255) NOT NULL,
  skill_level INT NOT NULL,
  team VARCHAR(255) NOT NULL,
  FOREIGN KEY (team) REFERENCES teams (team_name)
  PRIMARY KEY (player_id)
);

-- Games table
CREATE TABLE games (
  game_id INT NOT NULL AUTO_INCREMENT,
  host_team_name VARCHAR(255) NOT NULL,
  guest_team_name VARCHAR(255) NOT NULL,
  game_time DATETIME NOT NULL,
  score INT,
  PRIMARY KEY (game_id),
  FOREIGN KEY (host_team_id) REFERENCES teams (team_name),
  FOREIGN KEY (guest_team_id) REFERENCES teams (team_name)
);

-- Injuries table
CREATE TABLE injuries (
  injury_id INT NOT NULL AUTO_INCREMENT,
  player_id INT NOT NULL,
  injury_type VARCHAR(255) NOT NULL,
  injury_severity VARCHAR(255) NOT NULL,
  PRIMARY KEY (injury_id),
  FOREIGN KEY (player_id) REFERENCES players (player_id)
);

```


 