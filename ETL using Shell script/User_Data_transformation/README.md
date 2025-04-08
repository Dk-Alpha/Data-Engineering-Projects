
![Bash](https://img.shields.io/badge/Shell-Bash-blue.svg) ![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue)

# ETL using Shell Scripting

## 📅 Overview
This project implements an **ETL (Extract, Transform, Load)** pipeline using **shell scripting** and **PostgreSQL**.
We automate the process of downloading a log file, extracting relevant fields, transforming the format, and loading the cleaned data into a PostgreSQL database.

---

## 🔢 Project Workflow

### 1. 🔄 Download the Data
- Downloaded the compressed file `web-server-access-log.txt.gz` using `wget`.

### 2. 🔀 Extract the File
- Decompressed the `.gz` file using `gunzip` to obtain `web-server-access-log.txt`.

### 3. 🧐 Extract Specific Columns
- Extracted the first four fields (**timestamp, latitude, longitude, visitorid**) from the file using `cut`.
- Saved the output into `extracted-data.txt`.

### 4. ✨ Transform the Data
- Replaced the `#` delimiter with `,` using the `tr` command.
- Saved the result as `transformed-data.csv`.

### 5. 🔫 Setup PostgreSQL Database
- Connected to the `template1` database.
- Created a table `access_log` with the following structure:
```sql
CREATE TABLE access_log (
    timestamp TIMESTAMP,
    latitude FLOAT,
    longitude FLOAT,
    visitor_id CHAR(37)
);
```

### 6. 🛋️ Load the Data
- Used the `COPY` command through `psql` to import `transformed-data.csv` into the `access_log` table.
- The `HEADER` option was enabled to handle the CSV's first row.

### 7. ✨ Full Automation
- All steps are encapsulated into a single shell script named `cp-access-log.sh`.
- Run the script once to perform the complete ETL process.

---

## 🗋 Files Included

| File Name               | Description                                       |
|--------------------------|---------------------------------------------------|
| `cp-access-log.sh`       | Bash script to perform the ETL operations         |
| `extracted-data.txt`     | Extracted raw data from the access log            |
| `transformed-data.csv`   | Transformed CSV ready for database import         |
| `access_log` (PostgreSQL table) | Final table storing structured data      |

---

## 🔧 Technologies Used
- **Shell Scripting (Bash)**
- **PostgreSQL**
- **Linux CLI tools**: `wget`, `gunzip`, `cut`, `tr`, `psql`

---

## 🔍 How to Run It

1. Ensure PostgreSQL server is running.
2. Open terminal.
3. Execute:
```bash
bash cp-access-log.sh
```
4. Verify the database entry:
```sql
\c template1;
SELECT * FROM access_log;
```

Example output:
```
        timestamp        | latitude | longitude |              visitor_id
--------------------------+----------+-----------+--------------------------------------
 2019-04-29 09:13:47.177  |   37.785 |  -122.406 | b3e4d42c-3847-41ed-85ed-58a62a2fcf99
...
```

---

## 🔹 Key Commands Explained
- `wget`: Downloads files from web servers.
- `gunzip`: Decompresses `.gz` files.
- `cut`: Extracts specific fields.
- `tr`: Replaces characters.
- `psql`: Interacts with PostgreSQL database.

---

## 💡 Learning Highlights
- Practical ETL automation using bash scripting.
- Basic database design and bulk data loading.
- Hands-on practice with file manipulation commands.
- Understanding real-world data transformation workflows.

---

### 💚 Thank you for checking out this project!

---

> **Note**: If you face any permission issues during `psql` execution from the script, ensure your PostgreSQL user has appropriate rights and that you modify the script's paths if needed based on your environment.
