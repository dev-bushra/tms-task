# tms-task

.env:
DB_HOST=localhost
DB_PORT=5432
DB_NAME=tms
DB_USER=postgres
DB_PASSWORD=postgres
JWT_SECRET=bushratv


db:
CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    due_date DATE NOT NULL,
    priority VARCHAR(50) NOT NULL,
    status VARCHAR(50) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

--

INSERT INTO tasks (user_id, title, description, due_date, priority, status) VALUES
    (1, 'Finish library project', 'Complete the backend for the library management system.', '2025-05-05', 'high', 'pending'),
    (2, 'Update frontend UI', 'Improve the design and make it responsive.', '2025-05-10', 'medium', 'pending'),
    (3, 'Write unit tests', 'Write unit tests for the task management API.', '2025-05-15', 'low', 'pending'),
    (4, 'Deploy backend to production', 'Deploy the library management system to production.', '2025-06-01', 'high', 'completed');
INSERT INTO users (name, email, username, password) VALUES
    ('John Doe', 'john.doe@example.com', 'johndoe', 'hashedpassword1'),
    ('Jane Smith', 'jane.smith@example.com', 'janesmith', 'hashedpassword2'),
    ('Emily Johnson', 'emily.johnson@example.com', 'emilyjohnson', 'hashedpassword3'),
    ('Michael Brown', 'michael.brown@example.com', 'michaelbrown', 'hashedpassword4');


