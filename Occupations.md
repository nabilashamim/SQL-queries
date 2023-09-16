select CONCAT(occ.name,'(',(LEFT(occ.occupation,1)),')')
from occupations occ  
group by occ.name, occ.occupation
order by occ.name, occ.occupation;

select CONCAT('There are a total of ',
            COUNT(occupation),' ', lower(occupation),'s.')
from occupations group by occupation
order by COUNT(occupation),occupation;
