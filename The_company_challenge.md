SELECT
    c.company_code AS company_code,
    c.founder AS Founder,
    count(distinct e.lead_manager_code) AS total number LM,
    count(distinct e.senior_manager_code) AS total number SM,
    count(distinct e.manager_code) AS total number M,
    count(distinct e.employee_code) AS total number E
From company c
inner join employee e
    on e.company_code = c.company_code
group by c.company_code, c.founder
order by company_code;
