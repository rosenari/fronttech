#### 버블링

- 한 요소에 이벤트가 발생하면 요소에 할당된 핸들러가 동작하고, 이어서 부모의 핸들러도 동작합니다.
- 가장 최상위 부모를 만날때까지 위 과정이 반복되며, 각각 할당된 핸들러가 동작합니다.

```html
<style>
    body * {
        margin: 10px;
        border: 1px solid blue;
    }
</style>

<form onclick="alert('form')">FORM
    <div onclick="alert('div')">DIV
        <p onclick="alert('p')">P</p>
    </div>
</form>
```

> p를 클릭하면 alert('p') => alert('div') => alert('form') 순으로 실행됩니다.
> div를 클릭하면 alert('div') => alert('form') 순으로 실행됩니다.
> form을 클릭하면 alert('form')만 실행됩니다.

#### event.target과 event.currentTarget의 차이

- event.target은 실제 이벤트가 발생한 가장안쪽 요소입니다.
- this(event.currentTarget)는 현재 실행중인 핸들러가 할당된 요소입니다. 

```html
<style>
    body * {
        margin: 10px;
        border: 1px solid blue;
    }
</style>

<form>FORM
    <div>DIV
        <p>P</p>
    </div>
</form>

<script>
    form.onclick = function(event){
        event.target.style.backgroundColor = "yellow";
        
        setTimeout(()=> {
            alert('target='+event.target.tagName+" ,this="+this.tagName); 
            event.target.style.backgroundColor = '';
        },0);
    }
</script>
```

> this.tagName은 항상 FORM이다.
> event.target.tagName은 클릭한 태그가 표시될 것이다.

### 버블링 중단하기
- 버블링은 이벤트가 발생한 요소부터 최상위 요소까지 핸들러가 동작하는 개념입니다.
- 핸들러에 이벤트 처리후 버블링을 중단하도록 명령 할 수도 있습니다.
- event.stopPropagation()을 사용하면 해당 요소에서 버블링이 멈추고 상위요소로 전파되지 않습니다.

```
<body onclick="alert('no reachable')">
    <button onclick="event.stopPropagation()">클릭해주세요.</button>
</body>
```

> alert('no reachable')은 실행되지 않습니다.