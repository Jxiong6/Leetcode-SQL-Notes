### [175. 组合两个表](https://leetcode.cn/problems/combine-two-tables/)

```sql
select P.firstName , P.lastName, A.city, A.state
from Person P left join Address A on P.PersonID = A.PersonID
```

> Note: 

left join ： 保留left table 全部数据

right join  ：保留right table 全部数据

inner join ：取两表公共数据



### [181. 超过经理收入的员工](https://leetcode.cn/problems/employees-earning-more-than-their-managers/)



``` sql
select e1.name Employee
from Employee e1 ,Employee e2 
where e1.ManagerId = e2.Id and e1.salary >  e2.salary
```



>Note:
>
>或者使用Join： 
>
>```sql
>SELECT
>     a.NAME AS Employee
>FROM Employee AS a JOIN Employee AS b
>     ON a.ManagerId = b.Id
>     AND a.Salary > b.Salary
>;
>```



### [182. 查找重复的电子邮箱](https://leetcode.cn/problems/duplicate-emails/)

```sql
select email as Email
from Person
group by Email 
having count(Email) >1
```



### [183. 从不订购的客户](https://leetcode.cn/problems/customers-who-never-order/)

```sql
select a.name as Customers
from Customers a left join Orders b on a.id = b.customerId 
where b.customerId is null 
```



### [511. 游戏玩法分析 I](https://leetcode.cn/problems/game-play-analysis-i/)

```sql
select player_id, min(event_date) first_login
from activity
group by player_id

```



### [586. 订单最多的客户](https://leetcode.cn/problems/customer-placing-the-largest-number-of-orders/)

```sql
select customer_number
from Orders 
group by customer_number
order by count(*) desc
limit 1
```



>note : 

desc 降序  asc 升序 





###  [607. 销售员](https://leetcode.cn/problems/sales-person/)

```sql
SELECT  s.name
FROM SalesPerson s
where s.sales_id not in
(SELECT o.sales_id
FROM Orders AS o join Company AS c on o.com_id = c.com_id
where c.name = 'RED')

```

> note:

子查询 

### [627. 变更性别](https://leetcode.cn/problems/swap-salary/)

```sql
# 1.
UPDATE Salary 
set 
sex = case sex when 'm' then 'f' else 'm' end 

# 2.
update salary set sex = if(sex='m','f','m');
```



>note:  动态设置 可以在使用CASE... WHEN... 的时候同时使用UPDATE语句
>
>case...when...



```sql
case 列名 
	when ..then ..
	when ..then ..
	else..
end 
```

UPDATE： 

```sql
update 表名
set 列名 = 修改后的值；
```



### [1050. 合作过至少三次的演员和导演](https://leetcode.cn/problems/actors-and-directors-who-cooperated-at-least-three-times/)

```sql
select actor_id, director_id 
from actordirector
group by actor_id, director_id
having count(*)>=3
```



### [196. 删除重复的电子邮箱](https://leetcode.cn/problems/delete-duplicate-emails/)

```sql
DELETE a
FROM Person a, Person b
WHERE a.id >b.id  and a.email = b.email
```

> note：自连接例子：
>
>  ![test](./images/image-20240428224238263.png)
>
> 
>
> 
>
> sql执行顺序 ： FROM > WHERE > GROUP BY > HAVING > SELECT >DISTINCT > ORDER BY > LIMIT/OFFSET 

### [197. 上升的温度](https://leetcode.cn/problems/rising-temperature/)

``` sql
select  a.id
from weather as a , weather as b 
where datediff(a.recordDate, b.recordDate) =1 
and a.Temperature > b.Temperature
```



> note:
>
> DATEDIFF(endDate, startDate) -- 返回两个日期之间的天数差异
>
> TIMEDIFF(time1, time2) -- 计算两个时间之间的差异
>
> DATE_ADD(date, INTERVAL expr type), DATE_SUB() -- 在日期上加上或减去一个指定的时间间隔



### [577. 员工奖金](https://leetcode.cn/problems/employee-bonus/)

```sql 
select e.name, b.bonus
from Employee as e left join  Bonus as b on e.empId = b.empId 
where b.bonus < 1000 or b.bonus is null
```



###  [584. 寻找用户推荐人](https://leetcode.cn/problems/find-customer-referee/)

```sql
select name 
from customer 
where referee_id !=2 or referee_id is null 
```



### [595. 大的国家](https://leetcode.cn/problems/big-countries/)

```sql
select name,population, area
from world
where area >= 3000000 or population >= 25000000
```





### [596. 超过5名学生的课](https://leetcode.cn/problems/classes-more-than-5-students/)

```sql
select class
from courses 
group by class 
having count(student) >=5
```



### [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/)

```sql
SELECT x, y, z , if(x + y > z and x + z > y and y + z > x ,'Yes', 'No') as triangle 
FROM Triangle 
```



> note:
>
> Mysql中使用if ：
>
> ```sql
> IF(expression, value_if_true, value_if_false)
> ```



### [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/)

```sql
select max(num) as num
from (select num
	  from MyNumbers 
      group by num 
      having count(*) =1 ) as new 

```

> note: 
>
> ![](./images/4714ca5f6692c6f5c4b9948cfc890d6.png)



### [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/)

```sql
select *
from Cinema 
where id%2 =1 and description != 'boring'
order by rating desc
```

> note:
>
> is not 和!=的区别 =》 !=用于两个非null值不相等时返回true , is not 通常用于特殊比较is not null ； is not true 
>
> 例如：
>
> ```sql
> select true is not true #会返回0
> select false is not true #会返回1 
> ```



### [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)



```sql
select p.product_name, s.year ,s.price 
from sales as s join product as p on s.product_id = p.product_id 
```



### [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/)



```sql
select project_id , round(avg(experience_years),2) as average_years
from project as p join employee as e on p.employee_id = e.employee_id
group by project_id  

```



### [1084. Sales Analysis III](https://leetcode.com/problems/sales-analysis-iii/) 

```sql
select p.product_id, p.product_name 
from product as p join sales as s on p.product_id = s.product_id 
group by s.product_id
HAVING MIN(s.sale_date) >= "2019-01-01" AND MAX(s.sale_date) <= "2019-03-31"
```

> note:
>
> 在使用group by 分组之后，having子句通常与聚合函数一起使用（SUM, AVG, MIN, MAX ）



### [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)

```SQL
select activity_date as day, count(distinct user_id) as active_users 
from Activity
where activity_date between '2019-06-28' and '2019-07-27' 
group by day

```

>NOTE:
>
>在group by 之前可以先使用where条件进行筛选。



### [1148. Article Views I](https://leetcode.com/problems/article-views-i/)

```sql
select distinct author_id as id 
from views
where author_id = viewer_id
order by author_id asc
```

### [1179. Reformat Department Table](https://leetcode.com/problems/reformat-department-table/)

```sql
SELECT id,
SUM(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue,
SUM(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue,
SUM(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue,
SUM(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue,
SUM(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue,
SUM(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue,
SUM(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue,
SUM(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue,
SUM(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue,
SUM(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue,
SUM(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue,
SUM(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department 
GROUP BY id
ORDER BY id;
```

>note : 
>
>```sql
>CASE
>    WHEN condition1 THEN result1
>    WHEN condition2 THEN result2
>    ...
>    ELSE resultN -- 可选
>END
>
>```



### [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/)

```sql
select query_name,round(sum(rating/position)/count(query_name),2) as quality ,round(sum(case when rating <3 then 1 else 0 end)/count(query_name)*100,2) as poor_query_percentage
from queries 
where query_name is not null
group by query_name
```





### [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/)

```sql
select  p.product_id,  COALESCE(round(sum(p.price*u.units)/sum(u.units),2),0) as average_price
from prices as p  left join unitssold u on p.product_id = u.product_id and u.purchase_date between p.start_date and p.end_date
group by p.product_id
```

> note:
>
> `COALESCE` 是一个 SQL 函数，用于从其参数列表中返回第一个非 `NULL` 值。如果所有给定的参数都是 `NULL`，则 `COALESCE` 函数也会返回 `NULL`。这个函数非常有用，特别是在处理可能包含 `NULL` 值的数据时，它可以帮助避免在应用逻辑上的错误或中断。





### [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/)

```sql
select new.student_id, new.student_name, new.subject_name, count(e.subject_name) as attended_exams
from
(select * from students cross join subjects) as new  left join examinations as e on new.student_id = e.student_id and new.subject_name = e.subject_name
group by new.student_id, new.subject_name
order by new.student_id, new.subject_name
```

> note:
>
> 题目中需要找到每个学生参加每项考试的数量
>
> 所以首先将包含student_id, student_name  的Students表 和包含subject_name的Subjects表进行cross join 成为new表
>
> ```sql
> select * from students cross join subjects
> ```
>
> 得到每个学生都和不同的学科有交集
>
> 然后使用left join 和包含student_id subject_name 的表Examinations。
>
> left join的条件是student_id subject_name 相同。 这样方便之后对参与科目的数量进行统计
>
> ```sql
> (select * from students cross join subjects) as new  left join examinations as e on new.student_id = e.student_id and new.subject_name = e.subject_name
> ```
>
> 然后使用
>
> ```sql
> group by new.student_id, new.subject_name
> order by new.student_id, new.subject_name
> ```
>
> 因为以上的group by
>
> 最后统计参与的次数使用count(e.subject_name)
>
> ```sql
> select new.student_id, new.student_name, new.subject_name, count(e.subject_name) as attended_exams
> from
> (select * from students cross join subjects) as new  left join examinations as e on new.student_id = e.student_id and new.subject_name = e.subject_name
> group by new.student_id, new.subject_name
> order by new.student_id, new.subject_name
> 
> ```



### [1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/)

```sql
select p.product_name,sum(o.unit) as unit
from products p join orders o on p.product_id = o.product_id 
where o.order_date between '2020-02-01' and '2020-02-29'
group by o.product_id
having sum(o.unit)>=100
```



### [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

```sql
select en.unique_id, e.name
from Employees e left join EmployeeUNI en on e.id = en.id 
```



### [1407. Top Travellers](https://leetcode.com/problems/top-travellers/)

```sql
select u.name, coalesce(sum(r.distance),0) as  travelled_distance 
from users u left join rides r on u.id = r.user_id 
group by u.id 
order by coalesce(sum(r.distance),0) desc, u.name asc 
```





### [1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/)

```sql
select sell_date, count(distinct product) as num_sold, group_concat(distinct product order by product asc separator ',') as products
from activities 
group by sell_date 
order by sell_date asc
```

> note:
>
> concat(str1,str,....)函数：将多个字符串连接成一个字符串
>
> concat_ws(separator，str1,str2,..)函数：分隔符不能为null
>
> group_concat ([distinct] 要连接的字段[ order by 排序字段 asc/desc ] [separator ' 分隔符'])：将group by产生的同一个分组中的值连接起来，返回一个字符串结果。



### [1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/)

```sql
select *
from Users
where mail  REGEXP '^[A-Za-z][A-Za-z0-9_\.\-]*@leetcode(\\?com)?\\.com$' 
```

> note: 
>
> 正则表达式：
>
> 反斜杠 `\\` 用来转义
>
> ^ : 从字符串开始匹配的regexp模式
>
> [A-Za-z] ： 匹配大小写
>
> [A-Za-z0-9_\\.\\-]*  ：匹配第一字母后的任意字符（大小写，数字，下划线，句号，破折号）
>
> (\\\\ ?com)? 使?com 成为可选项 允许模式同时匹配 "@leetcode.com "和"@leetcode?com"
>
> $： regex模式结束





### [1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/)

```sql
select *
from patients 
where conditions like '%_% DIAB1%' or conditions like 'DIAB1%'
```

> note:
>
> 通配符匹配： like '%_%' 
>
> - `%`：表示在字符串的开头或结尾可以包含任意数量的字符，或没有字符。
> - `_`：中间必须有一个字符。



### [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)

```sql
select Visits.customer_id, count(customer_id) as count_no_trans
from Visits  left join Transactions on Visits.visit_id=Transactions.visit_id
where transaction_id is null
group by customer_id
```





### [1587. Bank Account Summary II](https://leetcode.com/problems/bank-account-summary-ii/)



```SQL
select u.name as NAME, SUM(t.amount) as BALANCE
from Users u left join transactions t on u.account = t.account 
group by u.name
having sum(t.amount) > 10000
```





### [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/)

```sql
select r.contest_id, round((count(distinct r.user_id)*100)/(select count(user_id) from users),2) as  percentage
from register r  
group by r.contest_id
order by  percentage desc, contest_id asc 
```





### [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)

```sql
select a1.machine_id, round(avg(a2.timestamp - a1.timestamp),3) as processing_time
from activity a1 join activity a2 
on a1.machine_id = a2.machine_id and a1.process_id = a2.process_id and a1.activity_type = 'start' and a2.activity_type = 'end'
group by a1.machine_id

```

>note:
>
>count()括号里不能直接使用条件，但可以使用case when .. then.. else.. end 



### [1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/)

```sql
select user_id, concat(upper(left(name,1)),lcase(substring(name,2))) as name 
from users
order by user_id 
```

>note:
>
>upper()转换成大写 
>
>left（name，1）从左第一个
>
>lcase（）小写
>
>substring（name,2）从name第二个字符开始提取子字符串





### [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)

```sql
select tweet_id
from tweets 
where length(content)>15
```



### [1693. Daily Leads and Partners](https://leetcode.com/problems/daily-leads-and-partners/)

```sql
select date_id, make_name,count(distinct lead_id)as unique_leads,count(distinct partner_id) unique_partners
from dailysales 
group by date_id,make_name
```





### [1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/)

```sql
select user_id,count(follower_id) as followers_count
from followers
group by user_id
order by user_id asc
```



### [1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/)

```sql
select e1.employee_id, e1.name, count(e2.reports_to) as reports_count,round(avg(e2.age),0) as average_age
from employees e1 join employees e2 on e1.employee_id = e2.reports_to 
group by e2.reports_to
order by e1.employee_id
```



### [1741. Find Total Time Spent by Each Employee](https://leetcode.com/problems/find-total-time-spent-by-each-employee/)

```sql 
select event_day as day, emp_id, sum(out_time-in_time) as total_time 
from employees 
group by event_day, emp_id 
```



### [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
select product_id
from Products
where low_fats = 'Y' and recyclable = 'Y'
```



### [1789. Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee/)

```sql
SELECT employee_id, department_id 
FROM Employee
WHERE primary_flag = 'Y'UNION
SELECT employee_id, department_id 
FROM Employee
GROUP BY employee_id
HAVING COUNT(department_id) = 1;
```

> note:
>
> `UNION` 是用于合并两个或多个 `SELECT` 语句的结果集的操作符。`UNION` 会去除重复的行，但如果需要保留重复的行，可以使用 `UNION ALL`。





### [1795. Rearrange Products Table](https://leetcode.com/problems/rearrange-products-table/)

```sql
select product_id , 'store1' as store, store1 as price 
from Products
where store1 is not null 
union
select product_id , 'store2' as store, store2 as price 
from Products
where store2 is not null 
union
select product_id , 'store3' as store, store3 as price 
from Products
where store3 is not null 
```



### [1873. Calculate Special Bonus](https://leetcode.com/problems/calculate-special-bonus/)

```sql
select employee_id,case when employee_id%2 = 1 and name not like 'M%' then salary else 0 end as bonus
from employees
order by employee_id
```



> note:
>
> 使用字符匹配的时候用Like 或者 not like



### [1890. The Latest Login in 2020](https://leetcode.com/problems/the-latest-login-in-2020/)

```sql
select user_id,max(time_stamp) as last_stamp
from logins 
where time_stamp like '2020-%'
group by user_id
```



### [1965. Employees With Missing Information](https://leetcode.com/problems/employees-with-missing-information/)

```sql
select distinct employee_id 
from(select employee_id 
from employees
union
select employee_id
from salaries) as new 
where employee_id not in 
(select e. employee_id
from employees e join salaries s on e.employee_id = s.employee_id )
order by employee_id asc
```



### [1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/)

```sql
select employee_id
from employees
where manager_id not in (select distinct employee_id
from employees ) and salary< 30000
order by employee_id asc
```



### [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/)

```sql
select teacher_id,count(distinct subject_id) cnt
from teacher 
group by teacher_id
```

