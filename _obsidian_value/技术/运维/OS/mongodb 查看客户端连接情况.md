```
db.currentOp()

db.currentOp(true).inprog


db.currentOp(true).inprog.forEach(
function(opDoc){//opDoc其实是返回的每个op操作对象
    printjson(opDoc['host'])//打印信息
 }
)
```