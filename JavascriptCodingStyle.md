# Javascript Coding style

## Naming conventions
全域要 Pascal case  
其餘則 camel case  
命名必須有意義  
```javascript
const Case = "b";

function updateCase(case){
    const newCase = "c";
}
```

如果是要模組化的 js file，只有 default 需要 Pascal case，其他都 camel case
```javascript
const OptionService = {};

OptionService.option1 = [];

const option1 = OptionService.option1;

export default OptionService;

export {
    option1
}
```

## Layout conventions
宣告一行一行寫   
❌
```javascript
var name="Eileen", score=25, flag="true";
```
✔️
```javascript
var name="Eileen";
var score =25;
var flag="true";
```

請善用 `if return`  
❌
```javascript
function myFn(input) {
	if (input) {
      // do something
	}
}
```
✔️
```javascript
function myFn(input) {
	if (!input) {
        return;
	}

    // do something
}
```

`return` 和 `throw` 該行必須往上空一行，除非該scope只有`return` 或 `throw` 那行  
❌
```javascript
function myFn(input) {
    let result = "Ok";
    result = "Ok" + input;
    return result;
}
```
❌
```javascript
function myFn(input) {
    if(!input){
        input = "No";
        throw new Error(input);
    }
}
```
✔️
```javascript
function myFn(input) {
    let result = "Ok";
    result = "Ok" + input;

    return result;
}
```
✔️
```javascript
function myFn(input) {
    if(!input){
        input = "No";

        throw new Error(input);
    }
}
```

### function 之間要空一行
❌
```javascript
function getData (){
	// some code
}
const getOtherData = async ()=>{
	// some code
}
```
✔️
```javascript
function getData (){
	// some code
}

const getOtherData = async ()=>{
	// some code
}
```

### 字串請使用雙引號
❌
```javascript
let a = '123';
```
✔️
```javascript
let a = "123";
```

### 該段程式碼結尾，要加上分號
❌
```javascript
let a = '123'
```
✔️
```javascript
let a = "123";
```

## Commenting conventions
### 註解(`//`)都必須使用新的一行，不要把註解寫在 code 後面   
❌
```javascript
const Case = "b"; // 不要寫註解在這
```
✔️
```javascript
// 寫註解在這
const Case = "b";
```

### 註解符號後面都要空一格
❌
```javascript
//The following declaration creates a query. It does not run
//the query.
```
✔️
```javascript
// The following declaration creates a query. It does not run
// the query.
```

### 註解上方必須空一行，除非是該scope第一行
❌
```javascript
function test () {
    const a = "a";
    // 註解上方要空一行
    const b = "b";
}
```
✔️
```javascript
function test () {
    const a = "a";

    // 註解上方要空一行
    const b = "b";
}
```
#### 但是`VUE`在宣告 `ref` 或 `computed` 或 `import`，可以免除這項規則
❌
```javascript
// OtpStatus原始資料
const OtpStatusData = ref([]);
const endDateDisplay = ref('');
const beginDateDisplay = ref('');
// 依條件篩選
const filterByNationalId = computed(() => otpStatusData.value.filter((data) => data.nationalId.includes(nationalId.value)));
const filterByPhone = computed(() => filterByNationalId.value.filter((data) => data.phone.includes(phone.value)));
const filterByConfirmIP = computed(() => filterByPhone.value.filter((data) => data.confirmIP.includes(confirmIP.value)));
```

✔️
```javascript
// OtpStatus原始資料
const OtpStatusData = ref([]);
const endDateDisplay = ref('');
const beginDateDisplay = ref('');
// 篩選input
const nationalId = ref("");
const phone = ref("");
const confirmIP = ref("");

// 依條件篩選
const filterByNationalId = computed(() => otpStatusData.value.filter((data) => data.nationalId.includes(nationalId.value)));
const filterByPhone = computed(() => filterByNationalId.value.filter((data) => data.phone.includes(phone.value)));
const filterByConfirmIP = computed(() => filterByPhone.value.filter((data) => data.confirmIP.includes(confirmIP.value)));
```
