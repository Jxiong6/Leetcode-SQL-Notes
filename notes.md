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

