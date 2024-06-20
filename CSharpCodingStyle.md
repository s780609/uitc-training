# CSharp Coding style

## 命名規則
### Pascal 大小寫
在命名類（class）、記錄（record）或結構（struct）時，使用 Pascal 大小寫（"PascalCasing"）。

```C#
public class DataService
{
}
```
```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```
```C#
public struct ValueCoordinate
{
}
```
在命名介面（interface）時，除了使用 Pascal 大小寫外，還需要在名稱前加上字母 I，以明確表示這是一個介面。

```C#
public interface IWorkerQueue
{
}
```

在命名類型的公有成員（例如字段、屬性、事件、方法和局部函數）時，使用 Pascal 大小寫。
```C#
public class ExampleEvents
{
    // A public field, these should be used sparingly
    public bool IsValid;

    // An init-only property
    public IWorkerQueue WorkerQueue { get; init; }

    // An event
    public event Action EventProcessing;

    // Method
    public void StartEventProcessing()
    {
        // Local function
        static int CountQueueItems() => WorkerQueue.Count;
        // ...
    }
}
```

私有方法也用 Pascal case
```C#
 // Method
    private void StartEventProcessing()
    {
        // ...
    }
```

在編寫位置記錄（positional records）時，對參數使用 Pascal 大小寫，因為它們是記錄的公有屬性。

```C#
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);
```
有關位置語法的更多信息，請參閱屬性定義的位置語法。

Camel case
在命名私有或內部字段時，使用 Camel 大小寫（"camelCasing"），並在名稱前加上下劃線 _。

```C#
public class DataService
{
    private IWorkerQueue _workerQueue;
}
```
提示：

在支持語句完成（statement completion）的 IDE 中編輯遵循這些命名約定的 C# 代碼時，輸入 _ 將顯示所有對象範圍內的成員。

在編寫方法參數時，使用 Camel 大小寫。
```C#
public T SomeMethod<T>(int someNumber, bool isValid)
{
}
```
有關 C# 命名約定的更多信息，請參閱 [C# Coding Style](https://github.com/dotnet/runtime/blob/main/docs/coding-guidelines/coding-style.md).

其他命名約定
不包含 using 指令的示例使用命名空間限定。如果你知道某個命名空間已在項目中默認導入，則不必完全限定該命名空間中的名稱。如果名稱過長而無法放入一行，可以在點（.）後面換行，如以下示例所示。

```C#
var currentPerformanceCounterCategory = new System.Diagnostics.PerformanceCounterCategory();
```

Only private fields, local variables and parameters to methods start with a lower-case letter
```C#
public class ResponseModel {
    private string messageOne {get;set;}
    private string messageTwo {get;set;}

    private void TestOne(string first){
        string firstString = string.Empty;
    }
}
```

不必更改使用 Visual Studio 設計工具創建的對象名稱以適應其他指南。

### 例外
當需要建立跟外部的`JSON`字串做轉換的class model時，可以忽略Pascal case和camel case，可以照者外部給予的欄位名稱來建立屬性
例如有一個外部API給予下列字串
```Json
{"msg":"","rc2":"M000"}
```
則可以建立物件
```C#
public class ResponseModel {
    public string msg {get;set;}
    public string rc2 {get;set;}
}
```

## Layout conventions
`return` 和 `throw` 的上方必須空一行，除非是該scope第一行
```C#
public string SomeMethod(string input)
{
    string a = "" + input;

    return a;
}
```

`if` and `for loop` block 結束後，要空一行
```C#
public void SomeMethod(string input)
{
    string a = "" + input;

    if (string.IsNullOrEmpty(a)) {
        a = "do something";
    }

    for (int i = 0; i < 10;i++) {
        a += i.ToString();
    }

    a = "do something" + "number 2";
}
```

### if, else if, else 一律用{}, 除非只有一個 if block且只有一行
❌
```C#
bool a = true;
string b = "";
if(a == true)
    b = "b";
else if(a == false)
    b = "b";
```
❌
```C#
if (!businessRelationshipsIsEight)
    return new ResultDto<CallEaiHubAndValidateDataDto>()
    {
        Code = ResponseCode.GetDataButNoRelationContract.ToStringType(),
        Message = ResponseCode.GetDataButNoRelationContract.ToDescriptionString(),
    };
```
✔️
```C#
bool a = true;
string b = "";
if(a == true)
{
    b = "Ok";
}
else if(a == false)
{
    b = "b";
}
```
✔️
```C#
bool a = true;
string b = "";

// 只有一個 if scope 且只有一行
if(a == true)
    b = "b";
```

### public method 要加寫 summary 註解 [建議 不強制]
❌
```C#
public string Test (string input) {
    return "OK";
}
```
✔️
```C#
/// <summary>
/// 把說明寫清楚方便別人使用你的方法
/// </summary>
/// <param name="input"></param>
/// <returns>返回處理後的結果，例: 成功 => "Ok"</returns>
public string Test (string input) {
    return "OK";
}
```

### `var` 使用規則，要可以在後面明顯看到該型別
❌
```C#
var a = GetUser(id);
```
✔️
```C#
var a = GetUser<Users>(id);
```

## Commenting conventions

### 註解(`//`)都必須使用新的一行，不要把註解寫在 code 後面   
❌
```C#
var Case = "b"; // 不要寫註解在這
```
✔️
```C#
// 寫註解在這
var Case = "b";
```

### 註解符號後面都要空一格
❌
```C#
//The following declaration creates a query. It does not run
//the query.
```
✔️
```C#
// The following declaration creates a query. It does not run
// the query.
```

### 註解上方必須空一行，除非是該scope第一行，除非是宣告物件屬性
❌
```C#
public string Test (string input) {
    var a = "a" + input;
    // 註解上方要空一行
    var b = "b";
}
```
✔️
```C#
public string Test (string input) {
    var a = "a" + input;

    // 註解上方要空一行
    var b = "b";
}
```
✔️
```
var a = new Users()
{
    public string Name {get; set;}
    // 宣告物件時，需要註解，不需要往上方空一行
    public string Account {get; set;}
}
```
