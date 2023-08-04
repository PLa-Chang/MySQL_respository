
# a表作为第一个数字，b表作为第二个数字，c表作为第三个数字. 用join把他们连接起来，而后判断连续的三个数字Num是否相同
select distinct l1.num as ConsecutiveNums 
from logs l1 
  join logs l2 on l1.id+1 = l2.id 
  join logs l3 on l2.id+1 = l3.id
where 
  l1.num = l2.num = l3.num;
