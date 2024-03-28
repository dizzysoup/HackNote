# JSON injection 
JSON 惡意注入攻擊


https://www.invicti.com/learn/json-injection/

中文文章：

https://ithelp.ithome.com.tw/articles/10253313


## Client 端
Client 端使用eval來接收json資料，容易使用JSON注入來加XSS在裡面

範例：
```javascript
    var result = eval("(" + json_string + ")");
    document.getElementById("#accountType").innerText = result.account;
    document.getElementById("#userName").innerText = result.name; 
    document.getElementById("#pass").innerText = result.pass;
```

attacker 可以在#accountType 插入：
```
    user"});alert(document.cookie);({"accountType":"user
```


## Server 端
如果伺服器使用者資料儲存成JSON字串，包括帳戶類型。
且使用者名稱密碼直接從輸入參數中獲取不彥鄭清裡的話，
惡意使用者將資料附加到輸入表中，或是HTTP Header 傳遞的使用者名稱
```
    john%22,%22accountType%22:%22administrator%22
```
後端接收的json 格式就會變成
```json
    {
        "accountType":"user",
        "userName":"john",
        "accountType":"administrator",
        "pass":"password"
    }
```
accountType 重複了，JSON會接收最後一個accountType，意外更改到最高權限的密碼
竄改密碼成功