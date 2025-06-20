
# 사용 이유
기존 DOM조작 방법은 코드가 길\~~긴했다. 
jQuery를 사용하면 기존 코드를 보다 짧고 간결하게 사용할 수 있지만
내 생각에는 jQuery를 모르는 사람이 보면 코드 분석은 힘들 것 같다.
내가 그랬기 때문이다. 그래서 오늘은 제이쿼리를 공부해보자아


---

## 사용법
jQuery cdn 검색 후 사용할 버전을 선택하고 `minified` 클릭하면 제이쿼리를 사용할 수 있는 스크립트가 나온다.
```
<script src="https://code.jquery.com/jquery-3.7.1.min.js" integrity="sha256-/JqT3SQfawRcv/BIHPThkBvs0OEvtFFmqPF/lYI/Cxo=" crossorigin="anonymous"></script>
```
자신의 html에 붙여넣어 사용.

```
$(document).ready(() =>{
	대부분 jQuery는 이 함수 내부에서 작성하는 것으로 한다.
	문서의 모든 요소가 로드된 후 jQuery 코드가 실행되는 것이 보장되기 때문
})
```


---

### 문법 변화 

`document.querySelector()` →  `$()` 
`document.querySelectorAll()` →  `$()` 
`addEventListener()` → `on()`
jQuery를 사용해서 dom조작 시 html 메소드를 사용해야 한다.

`innerHtml()` X
`html()` O

---
### 실습 코드


```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <script src="https://code.jquery.com/jquery-3.7.1.min.js" integrity="sha256-/JqT3SQfawRcv/BIHPThkBvs0OEvtFFmqPF/lYI/Cxo=" crossorigin="anonymous"></script>

</head>

<body>
    <p id="title">title</p>

	<p class="hello">hello</p>
    <p class="hello">hello</p>
    <p class="hello">hello</p>
 
    <button id="removeClassBTN">removeClass</button>
    <button id="modalBTN">modal</button>
    <button id="fadeOutBTN">fadeOut</button>
    <button id="fadeInBTN">fadeIn</button>
    <button id="toggleBTN">toggle</button>
</body>

<script>

    $(document).ready(() =>{
        $('#toggleBTN').on('click',()=>{

            $('.hello').fadeToggle();

        })

        $('#fadeOutBTN').on('click',()=>{

            $('.hello').fadeOut();

        })

        $('#fadeInBTN').on('click',()=>{

            $('.hello').fadeIn();

        })

  

        $('#title').addClass('hello')

        $('.hello').html('hi').css('color','red');

        $('#removeClassBTN').on('click',()=>{

            $('#title').removeClass('hello');

            $('#title').css('color','');

        })

        $('#modalBTN').on('click',()=>{

            alert('modal')

        })

    })

</script>
</html>
```