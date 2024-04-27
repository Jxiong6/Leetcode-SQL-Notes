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

