with totalscore as (
    select
        s.hacker_id,
        s.challenge_id,
        max(s.score) AS max_score
    from submissions s
    group by challenge_id, hacker_id
)
select
    h.hacker_id,
    h.name,
    sum(max_score)
from totalscore ts
join hackers h
on ts.hacker_id = h.hacker_id
group by h.hacker_id, h.name
having sum(max_score) > 0
order by sum(max_score) desc, h.hacker_id;
