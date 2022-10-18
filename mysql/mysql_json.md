# mysql json array字段排序问题

### 表结构例如
```
college_rank

[
  {"rank": "1", "rank_sub": [], "rank_name": "National Universities"}, 
  {"rank": "2", "rank_sub": [], "rank_name": "Best Value Schools"}, 
  {"rank": "1", "rank_sub": [
                               {"rank": "11", "rank_name_sub": "Chemical(tie)"}
                             ], "rank_name": "Best Undergraduate Engineering Programs"}, 
  {"rank": "3", "rank_sub": [
                              {"rank": "11", "rank_name_sub": "Artificial Intelligence(tie)"}, 
                              {"rank": "10", "rank_name_sub": "Biocomputing/Bioinformatics/Biotechnology"}, 
                              {"rank": "5", "rank_name_sub": "Programming Languages"}, 
                              {"rank": "4", "rank_name_sub": "Theory"}
                            ], "rank_name": "Computer Science(tie)"}, 
  {"rank": "9", "rank_sub": [], "rank_name": "First-Year Experiences"}, 
  {"rank": "1", "rank_sub": [], "rank_name": "Senior Capstone"}
]
[
  {"rank": "2", "rank_sub": [], "rank_name": "National Universities"}, 
  {"rank": "1", "rank_sub": [], "rank_name": "Best Value Schools"}, 
  {"rank": "2", "rank_sub": [
                              {"rank": "1", "rank_name_sub": "Aerospace /Aeronautical / Astronautical(tie)"}, 
                              {"rank": "4", "rank_name_sub": "Biomedical"}, 
                              {"rank": "1", "rank_name_sub": "Chemical"}, 
                              {"rank": "4", "rank_name_sub": "Civil"}, 
                              {"rank": "1", "rank_name_sub": "Computer(tie)"}, 
                              {"rank": "1", "rank_name_sub": "Electrical / Electronic / Communications"}, 
                              {"rank": "5", "rank_name_sub": "Environmental / Environmental Health(tie)"},
                              {"rank": "8", "rank_name_sub": "Industrial / Manufacturing"}, 
                              {"rank": "1", "rank_name_sub": "Materials"}, 
                              {"rank": "1", "rank_name_sub": "Mechanical"}
                            ], "rank_name": "Best Undergraduate Engineering Programs"}, 
  {"rank": "1", "rank_sub": [
                              {"rank": "2", "rank_name_sub": "Artificial Intelligence"}, 
                              {"rank": "2", "rank_name_sub": "Biocomputing/Bioinformatics/Biotechnology"}, 
                              {"rank": "2", "rank_name_sub": "Computer Systems"}, 
                              {"rank": "1", "rank_name_sub": "Cybersecurity(tie)"}, 
                              {"rank": "2", "rank_name_sub": "Data Analytics/Science"}, 
                              {"rank": "5", "rank_name_sub": "Game/Simulation Development(tie)"}, 
                              {"rank": "2", "rank_name_sub": "Mobile/Web Applications"}, 
                              {"rank": "2", "rank_name_sub": "Programming Languages"}, 
                              {"rank": "2", "rank_name_sub": "Software Engineering(tie)"}, 
                              {"rank": "1", "rank_name_sub": "Theory"}
                            ], "rank_name": "Computer Science(tie)"}, 
  {"rank": "4", "rank_sub": [], "rank_name": "Co-ops/Internships(tie)"}
]
```

```
select res.college_name, res.college_rank from(
select SUBSTRING_INDEX(JSON_UNQUOTE(JSON_SEARCH(college_rank, 'one', 'Best Value Schools')), '.', 1) as index_x, e.* from best_colleges.college as e ) as res
where res.index_x is not null
order by JSON_UNQUOTE(JSON_EXTRACT(res.college_rank, CONCAT(res.index_x,'.rank')));
```
