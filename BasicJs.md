# Basic Javascript

### Javascript
>  JavaScript ถูกพัฒนาโดยนาย Brendan Eich พนักงานจากบริษัท NetScape โดยชื่อแรกของมันคือ Mocha และถูกเรียกและเปิดตัวอย่างเป็นทางการในชื่อ LiveScript ก่อนจะมาเป็น JavaScript ในปัจจุบันครับ

>  หลายๆคนอาจจะยังเข้าใจผิดว่า JavaScript กับ ECMAScript คืออันเดียวกัน เพราะติดชื่อจำพวก ES6, ES7, ES2016 แต่จริงๆแล้วมันคนละตัวกันครับ ECMAScript เป็นมาตราฐานสำหรับภาษา Script ซึ่ง JavaScript นั้นถูกพัฒนาตามมาตราฐานนี้

### JSON
>  หรือ Java Script Object Notation เป็นโครงสร้างข้อมูลชนิดหนึ่ง ที่ทำให้ JavaScript แลกเปลี่ยนข้อมูลกับ Server 
#### EX

```javascript
  let users = [
  {
    "id": 1000,
    "name": "Corey Griffith",
    "username": "coGriffith",
    "gender": "male",
    "age": 13
  },
  {
    "id": 1001,
    "name": "Marion McDaniel",
    "username": "mMcDaniel",
    "gender": "female",
    "age": 15
  },
  {
    "id": 1002,
    "name": "Tom Robbins",
    "username": "tRobbins",
    "gender": "male",
    "age": 15
  },
  {
    "id": 1003,
    "name": "Ruth Harvey",
    "username": "rHarvey",
    "gender": "female",
    "age": 14
  },
  {
    "id": 1004,
    "name": "Terry Willis",
    "username": "tWillis",
    "gender": "male",
    "age": 13
  }
]
```
### ตัวแปรใน JavaScript
1. **var** คือ การประกาศตัวแปรสำหรับใช้ใน code ในส่วนที่ถูกรันในส่วนนั้นๆ อาจจะหมายถึงทั้ง function หรือทั้งไฟล์เลยก็เป็นได้

2. **let** คือ การประกาศตัวแปรสำหรับใช้เฉพาะใน scope นั้นหรือเฉพาะใน block นั้นๆ

3. **const** คือ การประกาศตัวแปรแบบค่าคงที่ หรือพูดง่ายๆคือตัวแปรแบบ Read Only

4. **ไม่ระบุ** คือ การประกาศแบบ global นั่นเองครับผม **การประกาศตัวแปรแบบ global คือการประกาศแบบใดก็ได้แต่เอาไว้ใน scope นอกสุดครับ**

#### Ex.1
```javascript
function varTest () {
  var x = 1;
  if (true) {
    var x = 2;  // มองเป็นตัวเดียวกันกับด้านนอก
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // มองเป็นคนละตัวกับด้านนอก
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
varTest()
letTest()
console.log(x) // error
```

#### Ex.2 
```javascript
function globalTest() {
  x = 1;
  if (true) {
    x = 2;
    console.log(x);  // 2
  }
  console.log(x);  // 2
}
globalTest()
console.log(x) // 2
```
#### Ex.3
```javascript
// ประกาศค่าคงที่ หรือ read only
const MY_VAR = 7;

// error
MY_VAR = 20;

// log 7
console.log(MY_VAR);

// error เพราะเป็น read only ประกาศใหม่ไม่ได้
const MY_VAR = 20;

// error
var MY_VAR = 20;

// error เช่นกัน
let MY_VAR = 20;
if (MY_VAR === 7) { 
  // ใช้ได้ครับ มันจะมองเป็นตัวแปร scoped แบบ let
  const MY_VAR = 20;

  // log 20
  console.log(MY_VAR);

  // error เพราะมันจะพยายามไปเปลี่ยน MY_VAR ของ global
  var MY_VAR = 20;
}
// log 7 เหมือนเดิม
console.log(MY_VAR);

```

### function ใน JavaScript
- มันสามารถเก็บลงตัวแปรได้
- สามารถส่ง function เป็น argument เข้าไปใน function อื่นๆได้
- สามารถ return ค่าออกมาเป็น function ก็ทำได้
#### Ex
```javascript
function main () {
  plusNumber1(5, 10, function(result) {
    console.log(result) // 15
  })
  console.log(plusNumber2(3,7))
}
function plusNumber1(num1, num2, callback) {
  callback(num1+num2)
}
function plusNumber2(num1, num2) {
  return num1+num2
}
main() // log 15 จากนั้น log 10
```
จะสังเกตว่า function plusNumber1 จะเป็นการบวกค่าให้และส่งค่ากลับด้วยการเรียก parameter ที่ชื่อ callback แต่ plusNumber2 จะ return ค่ากลับมาตรงๆเลย

ถ้าดูจาก code นั้นการที่จะเรียกใช้งาน plusNumber1 จะต้องส่ง function เข้าไปเป็น argument ตัวที่ 3 ซึ่ง function ที่ส่งเข้าไปนั้นจะรับ parameter 1 ตัวคือ result

เมื่อ plusNumber1 ทำงานเสร็จ ก็จะเรียกใช้ parameter ตัวที่ 3 ที่ส่งเข้ามา ซึ่งก็คือ function ที่ถูกส่งเข้ามานั่นเอง โดยเรียกใช้และส่งค่ากลับออกไป

### JavaScript กับ Asynchronous & Synchronous

1. **Synchronous** การสั่ง statement ให้ทำงานแบบ sequence หรือ ทำงานแบบเป็นลำดับจากบนลงล่าง หมายความว่า statement ที่มาก่อนจะถูกสั่งทำงานก่อน เมื่อเสร็จแล้วจึงจะสั่งทำงาน statement ถัดไป

2. **Asynchronous** การสั่งให้ statement นั้นๆทำงานเป็น sequence หรือทำงานแบบเป็นลำดับจากบนลงล่าง โดยไม่รอว่า statement ก่อนหน้าจะทำงานเสร็จแล้วหรือยัง

#### EX
```javascript
setTimeout(function () {
 console.log(‘first’)
}, 100)
console.log(‘second’) //log second ก่อนแล้ว log first
```
#### อธิบาย
1. คำสั่ง setTimeout ถูกสั่งทำงาน
2. setTimeout ถูก push ลง Queue Stack เพราะเป็น function เฉพาะ
3. คำสั่ง log(“second”) ถูกสั่งทำงาน
4. Engine สั่งพิมพ์ second ออกมาใน console
5. Engine ว่างจากงาน
6. Engine ดึง Event ที่อยู่ใน Queue Stack มาทำงานต่อ
7. Engine สั่ง setTimeout ทำงาน
8. Engine สั่งพิมพ์ first ออกมาใน console