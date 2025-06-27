    #SQL Project (hospital)

    #Tables  =  Patients , doctors and admission


###Show first name, last name, and gender of patients whose gender is 'M'

select first_name , last_name , gender from patients where gender  like 'M%';

###Show first name and last name of patients who does not have allergies. (null)

select first_name , last_name from patients where allergies is NULL;

###Show first name of patients that start with the letter 'C'

select first_name from patients where first_name like 'C%'

###Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

select first_name , last_name from patients where weight between 100 and 120;

###Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

update patients set allergies = "NKA" where allergies is NULL;

###Show how many patients have a birth_date with 2010 as the birth year.

select count(*) as total_patients from patients where year(birth_date) = 2010

###Show the first_name, last_name, and height of the patient with the greatest height.

select 
first_name , 
last_name, 
height 
from patients 
where height = (
select max (height) from patients)

###Show all the columns from admissions where the patient was admitted and discharged on the same day.

select * from admissions where admission_date = discharge_date

###Show the patient id and the total number of admissions for patient_id 579.

select  patient_id ,count (*) as total_addmission from admissions
where patient_id = 579

###Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

select 
first_name,
last_name , 
birth_date 
from patients 
where height > 160 
and weight > 70;

###Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

select
first_name , 
last_name , 
allergies 
from patients 
where allergies not NULL
and city is 'Hamilton'

###Show unique birth years from patients and order them by ascending.

select distinct year(birth_date) from patients order by birth_date asc

###Show unique first names from the patients table which only occurs once in the list.

select first_name  
from  patients
group by first_name
having count (first_name) = 1

###Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

select patient_id , first_name from patients where first_name like
's____%s';

###Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.

select 
p.patient_id,
p.first_name,
p.last_name 
from patients p
join admissions a  on p.patient_id = a.patient_id 
where diagnosis is  'Dementia'

###Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.

select 
(select  count(*) from patients where gender = 'M') as male_count,
(select  count(*) from patients where gender = 'F') as female_count;

###Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

select 
first_name , 
last_name , 
allergies
from patients
where allergies in ('Penicillin' , 'Morphine')
order by
allergies,
first_name ,
last_name;

###Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

select patient_id , diagnosis from admissions 
group by patient_id , diagnosis 
having count(*) > 1;

###Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.

select city , count(*) as num_patients from patients group by city 
order by num_patients desc , city asc

###Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.

select 
first_name , 
last_name , 
birth_date
from patients
where year(birth_date) between 1970 and 1979
order by birth_date asc

###Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

select province_id , sum (height) as sum_height from patients group by province_id 
having sum_height >= 7000 order by sum_height desc

###Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'

select (max(weight) - min(weight)) as weight_delta from patients where last_name is 'Maroni'




