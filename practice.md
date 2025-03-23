## Retrieve all hospitals' names and addresses

```sql
SELECT name, address
FROM hospitals;
```

## List all departments with their names and hospital names

```sql
SELECT d.name AS department_name, h.name AS hospital_name
FROM departments d
         JOIN hospitals h ON d.hospital_id = h.id;
```

## Show all doctors working in the "Cardiology" department.

```sql
SELECT d.name AS doctor_name, d.specialty
FROM doctors d
         JOIN departments dp ON d.department_id = dp.id
WHERE dp.name = 'Cardiology';
```

## Retrieve all patients' full names and email addresses.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name, email
FROM patients;
```

## List all appointments scheduled for today.

```sql
SELECT a.id, a.appointment_date, p.first_name AS patient_name, d.name AS doctor_name
FROM appointments a
         JOIN patients p ON a.patient_id = p.id
         JOIN doctors d ON a.doctor_id = d.id
WHERE a.appointment_date = CURDATE();
```

## Show all doctors and their respective specialties.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS doctor_name, specialty
FROM doctor;
```

## Retrieve patient records along with their medical diagnoses.

```sql
SELECT CONCAT(p.first_name, ' ', p.last_name) AS patient_name, m.diagnosis
from patient AS p
         JOIN medical_record AS m on p.id = m.patient_id;
```

## Show all appointments with patient names and doctor names.

```sql
SELECT concat(p.first_name, ' ', p.last_name) AS patient_name,
       concat(d.first_name, ' ', d.last_name) AS doctor_name,
       a.appointment_date,
       a.reason
FROM appointment a
         JOIN patient p ON a.patient_id = p.id
         JOIN doctor d ON a.doctor_id = d.id;
```

## Retrieve all appointments where the reason contains "fever".

```sql
SELECT *
FROM appointment
WHERE reason = 'fever';
```

## Show all male patients.

```SQL
SELECT *
FROM patient
WHERE gender = 'M';
```

# 🔎Filtering Data (WHERE, LIKE, BETWEEN, IN, DISTINCT)

## Retrieve all hospitals that have "Health" in their name.

```sql
SELECT name, address
FROM hospitals
WHERE name LIKE '%Health%';
```

## Get all patients whose first name starts with "A".

```sql
SELECT *
FROM patients
WHERE first_name LIKE 'A%';
```

## Retrieve doctors whose email domain is "@hospital.com".

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name, email
FROM doctor
WHERE email LIKE '%@hospital.com';
```

## Show all patients born between 1980 and 2000.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS patient_name, date_of_birth
FROM patient
WHERE YEAR(date_of_birth) BETWEEN 1980 AND 2000;
```

#### ------------------ or -------------------------

```sql
SELECT CONCAT(first_name, ' ', last_name) AS patient_name, date_of_birth
FROM patient
WHERE YEAR(date_of_birth) >= 1980
  AND YEAR(date_of_birth) <= 2000;
```

## Retrieve all doctors specializing in "Neurology" or "Orthopedics".

```sql
SELECT CONCAT(first_name, ' ', last_name) AS doctor_name, specialty
FROM doctor
WHERE specialty IN ('Neurology', 'Orthopedics');
```

## List unique doctor specialties available.

```sql
SELECT DISTINCT specialty
FROM doctor;
```

## Show all appointments scheduled between '2024-01-01' and '2024-06-30'.

```sql
SELECT *
FROM appointment
WHERE appointment_date BETWEEN '2024-01-01' AND '2024-06-30';
```

## Retrieve all departments that belong to hospital ID 2.

```sql
SELECT name
FROM departments
WHERE hospital_id = 2;
```

## Show all appointments that have a reason containing "pain".

```sql
SELECT *
FROM appointment
WHERE reason LIKE '%pain%';
```

## Retrieve patients who do not have a registered phone number.

```sql
SELECT *
FROM patient
WHERE phone_number IS NULL;
```

# 📊Sorting Data (ORDER BY)

## Retrieve all hospitals sorted by their establishment date (oldest first).

```sql
SELECT name, address, establishment_date
FROM hospitals
ORDER BY establishment_date;
```

## List all patients in alphabetical order by last name.

```sql
SELECT first_name, last_name
FROM patients
ORDER BY last_name;
```

## Show all doctors sorted by specialty.

```sql
SELECT *
FROM doctor
ORDER BY specialty;
```

## List appointments sorted by appointment date in descending order.

```sql
SELECT *
FROM appointment
ORDER BY appointment_date desc;
```

## Retrieve all medical records ordered by diagnosis alphabetically.

```sql
SELECT *
FROM medical_record
ORDER BY diagnosis;
```

# 🔢Aggregate Functions (COUNT, SUM, AVG, MAX, MIN)

## Count the total number of hospitals.

```sql
SELECT COUNT(*) AS total_hospitals
FROM hospitals;
```

## Find the number of doctors in each specialty.

```sql
SELECT specialty, COUNT(*) AS total_doctors
FROM doctor
GROUP BY specialty;
```

## Count the number of male and female patients.

```sql
SELECT gender, COUNT(id) as patients
FROM patient
GROUP BY gender;
```
