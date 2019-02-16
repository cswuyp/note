* [查询出一个科目成绩表中，平均分数大于80的所有学生信息](#查询出一个科目成绩表中，平均分数大于80的所有学生信息)



# 查询出一个科目成绩表中，平均分数大于80的所有学生信息
表里有课程名、学生名、分数几个字段  
1.方法一可以用逆向思维：先扫描表，查找出平均分数小于80的人的姓名，然后再次扫描表，用not in 
```
select distinct * from student A where A.name not in (select distinct s.name from student s where avg(s.score)<80)
```
2.方法二：
```
select * from student s group by s.name having avg(s.core)>=80
```
