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

> note：
>
> 自连接例子： 
>
> ![image-20240428224238263](C:\Users\xiong\AppData\Roaming\Typora\typora-user-images\image-20240428224238263.png)
>
> sql执行顺序 ： FROM > WHERE > GROUP BY > HAVING > SELECT >DISTINCT > ORDER BY > LIMIT/OFFSET 