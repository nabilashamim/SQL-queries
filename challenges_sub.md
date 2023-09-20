with challenge_counts AS(
    select
        hacker_id,
        count(*) AS challenge_created
    from challenges c
    group by hacker_id)
select 
    h.*,
    cc.challenge_created
from hackers h
join challenge_counts cc
    on h.hacker_id = cc.hacker_id
where
    case
    when cc.challenge_created = (select max(challenge_created)
    from challenge_counts)
    then true
    else
        not exists (
        select 1
        from challenge_counts
        where challenge_created = cc.challenge_created and hacker_id != cc.hacker_id)
    End
order by challenge_created desc, h.hacker_id;
