---
layout: post
title: "[JavaScript] localStorage 저장 예제"
date: 2019-05-25
excerpt: "localStorage 저장 예제"
tag:
- JavaScript
category: [JavaScript]
feature: https://kyounghwan01.github.io/lala/assets/img/title/bj_title.jpg
comments: false



---



## localStorage 저장 예제

간단한 로컬스토리지에 저장하는 예제입니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>local_ex</title>
  </head>
  <body>
    <input type="button" id="savebtn" value="save" onclick="saveMyStaff()" />
    <input type="button" id="loadbtn" value="load" onclick="load()" />
    <table>
      <tr>
        <td>1box<textarea name="1" id="1" cols="30" rows="10"></textarea></td>
        <td>2box<textarea name="2" id="2" cols="30" rows="10"></textarea></td>
        <td>3box<textarea name="3" id="3" cols="30" rows="10"></textarea></td>
      </tr>
      <tr>
        <td>
          1box_get<textarea name="1" id="4" cols="30" rows="10"></textarea>
        </td>
        <td>
          2box_get<textarea name="2" id="5" cols="30" rows="10"></textarea>
        </td>
        <td>
          3box_get<textarea name="3" id="6" cols="30" rows="10"></textarea>
        </td>
      </tr>
    </table>

    <script>
      let v1 = [];
      let v2 = [];
      let v3 = [];
      function saveMyStaff() {
          
        document.getElementById("savebtn").value = "저장됨";

        let v_1 = document.getElementById("1").value;
        v1.push(v_1);
        localStorage.setItem("k1", JSON.stringify(v1));
        v_1="";
        
        let v_2 = document.getElementById("2").value;
        v2.push(v_2);
        localStorage.setItem("k2", JSON.stringify(v2));
        let v_3 = document.getElementById("3").value;
        v3.push(v_3);
        localStorage.setItem("k3", JSON.stringify(v3));
      }
      function load(){
        document.getElementById("loadbtn").value = "읽음";
        let storedV1 = JSON.parse(localStorage.getItem('k1'));
        if(storedV1){
            document.getElementById(4).value = storedV1;
            // storedV1.forEach(function(){
            //     v1 = storedV1;
            // });
            v1 = storedV1;
        }
        let storedV2 = JSON.parse(localStorage.getItem('k2'));
        if(storedV2){
            document.getElementById(5).value = storedV2;
            v2 = storedV2;
        }
        let storedV3 = JSON.parse(localStorage.getItem('k3'));
        if(storedV3){
            document.getElementById(6).value = storedV3;
            v3 = storedV3;
        }

      }
      function init(){
        load();
      }init();
    </script>
  </body>
</html>

```

