* [查询出一个科目成绩表中，平均分数大于80的所有学生信息](#查询出一个科目成绩表中平均分数大于80的所有学生信息)



# 查询出一个科目成绩表中，平均分数大于80的所有学生信息

错误的SQL语句，在select加入了cn（课程号），如果要显示课程号会破坏查找，因为品骏分数是所有课程的而不是单个课程的，这样查出来的是单个课程的分数而不是平均分数
```
select cn,name,avg(score) from student group by cn,name having avg(s.core)>=80
```

```
select name avg(score) from student group by name having avg(score)>=80;
```
在group by 语句后面如果需要进行条件筛选添加having 条件语句，where后面不能加聚合函数例如avg，所以这里只能用group by  having
