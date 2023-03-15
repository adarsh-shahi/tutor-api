### 7 tables

1. users

```sql
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  email VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(500) NOT NULL,
  role DEFAULT, -- student
  name VARCHAR(40) NOT NULL,
  bio VARCHAR(400),
  avatar VARCHAR(200),
);
```

#

2. pending_roles

```sql
CREATE TABLE pendingRoles(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   name VARCHAR(40) NOT NULL,
   email VARCHAR(255) UNIQUE NOT NULL,
   password VARCHAR(500) NOT NULL,
   appliedRole varchar(10),
);
```

#

3. courses

```sql
CREATE TABLE courses(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   updated_at TIMESTAMP,
   teacher_id INTEGER NOT NULL ON DELETE SET NULL,
   name VARCHAR(100) NOT NULL,
   description VARCHAR(1000),
   image VARCHAR(200) NOT NULL,
   FOREIGN KEY(teacher_id) REFERENCES users(id),
);
```

#

4.  courses_videos

```sql
CREATE TABLE coursevideo(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   updated_at TIMESTAMP,
   course_id INTEGER NOT NULL ON DELETE CASCADE,
   name VARCHAR(100) NOT NULL,
   description VARCHAR(1000),
   image VARCHAR(200) NOT NULL,
   url VARCHAR(2048) NOT NULL,
   FOREIGN KEY(cource_id) REFERENCES cources(id)
);
```

#

5.  pending_course_video

```sql
CREATE TABLE pending_course_video(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   cource_id INTEGER NOT NULL ON DELETE CASCADE,
   name VARCHAR(100) NOT NULL,
   description VARCHAR(1000),
   image VARCHAR(200) NOT NULL,
   url VARCHAR(2048) NOT NULL,
   FOREIGN KEY(cource_id) REFERENCES cources(id)
);
```

#

6. ratings

```sql
CREATE TABLE ratings(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   updated_at TIMESTAMP,
   cource_id INTEGER NOT NULL ON DELETE CASCADE,
   user_id INTEGER NOT NULL ON DELETE CASCADE,
   rating INTEGER,
   FOREIGN KEY(cource_id) REFERENCES cources(id),
   FOREIGN KEY(user_id) REFERENCES users(id)
);
```

#

7. comments

```sql
CREATE TABLE comments(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   updated_at TIMESTAMP,
   user_id  INTEGER  NOT NULL ON DELETE CASCADE,
   video_id INTEGER NOT NULL ON DELETE CASCADE,
   content VARCHAR(1000),
   FOREIGN KEY(user_id) REFERENCES users(id),
   FOREIGN KEY(video_id) REFERENCES video(id)
);
```

8. reviews

```sql
CREATE TABLE reviews(
   id SERIAL PRIMARY KEY,
   created_at TIMESTAMP,
   updated_at TIMESTAMP,
   user_id  INTEGER UNIQUE NOT NULL ON DELETE CASCADE,
   cource_id INTEGER UNIQUE NOT NULL ON DELETE CASCADE,
   content VARCHAR(1000),
   FOREIGN KEY(user_id) REFERENCES users(id),
   FOREIGN KEY(cource_id) REFERENCES cources(id)
);
```
