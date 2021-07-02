##### top
# ``Javascript`` 기초지식 정리

##### 00
# 00. 목차

1. [브라우저 저장소 (``LocalStorage``, ``SessionStorage``, ``Cookie``)](#01)
2. [Javascript의 ``this``](#02)
3. [Javascript의 ``Event`` 동작방식](#03)
4. [Javascript 비동기 처리](#04)



<br/><hr/><br/>



##### 01
# 01. 브라우저 저장소 (``LocalStorage``, ``SessionStorage``, ``Cookie``)

브라우저 저장소는 특정 도메인에 관련된 데이터를 저장하는 공간 입니다.

종류는 다음과 같습니다.

* ``LocalStorage``
* ``SessionStorage``
* ``Cookie``

<br/>

브라우저 저장소의 공통사항은 다음과 같습니다.

* 클라이언트의 브라우저에 데이터를 저장 합니다.
* ``키/값`` 의 형태로 데이터를 저장 합니다.
* 브라우저 저장소에 저장할 실제 데이터는 ``문자열``로 변환하여 저장해야 합니다.

<br/>

## 01-01. ``Cookie``

``HTML5`` 이전 버전의 브라우저에는 ``Cookie``만 존재 하였습니다.

``HTTP`` 통신은 요청자에 대한 정보를 가지지 않기 때문에, 요청을 받은 서버가 응답할 때, ``응답 대상``을 알 수 없으므로 응답할 수 없는 구조 입니다.

따라서 ``HTML`` 통신에서 서버 요청 시, ``Cookie``에 요청자에 대한 정보를 담아 전달하고, 서버에서는 ``Cookie``로 받은 요청자 정보를 사용하여 ``응답`` 하게 됩니다.

<br/>

``Cookie``의 주 목적은 ``요청자 정보``를 알려주기 위함이었기에, 최대 용량은 ``4kb``로 제한 하였습니다.

또한 저장하는 데이터는 ``키/값``으로 구성되지만, 하나의 문자열로 통합된 형식으로 되어 있어서, ``정규식``을 사용한 필터작업으로 사용해야 하는 불편함이 있습니다.

<br/>

그리고 ``Cookie``는 저장된 데이터에 ``만료 기간``을 설정할 수 있으며, ``만료 기간``이 지나면 자동으로 ``삭제`` 됩니다.


<br/><br/>


## 01-02. ``LocalStorage``와 ``SessionStorage``

``LocalStorage``와 ``SessionStorage``는 ``HTML5``에서 추가된 브라우저 저장소 입니다.

두 저장소는 ``데이터 영구성``을 제외하면 동일한 특징을 가집니다.

<table border="1" style="text-align: center;">
  <tr>
    <th></th>
    <th>Local Storage</th>
    <th>Session Storage</th>
  </tr>

  <tr>
    <th>저장소 접근 방법</th>
    <td>window.localStorage</td>
    <td>window.sessionStorage</td>
  </tr>

  <tr>
    <th>데이터 형식</th>
    <td colspan="2">[키: 값] 형식</td>
  </tr>

  <tr>
    <th>저장 방식</th>
    <td colspan="2">데이터 저장시 문자열로 Parsing 필요: JSON.stringify()</td>
  </tr>

  <tr>
    <th>데이터 사용 방식</th>
    <td colspan="2">데이터 사용시 Parsing 필요: JSON.parse()</td>
  </tr>

  <tr>
    <th>용량</th>
    <td colspan="2">모바일: 2.5mb, PC: 5mb ~ 10mb</td>
  </tr>

  <tr>
    <th>데이터 유효기간</th>
    <td>삭제전까지 영구 저장</td>
    <td>Session 종료 시, 삭제</td>
  </tr>
</table>



<br/>

[🔺 Top](#top)

<hr/><br/>



##### 02
## 02. Javascript의 ``this``

Javascript 프로그램의 동작은 ``Execution Context (실행 컨텍스트)``의 개념을 베이스로 합니다.

``실행 컨텍스트``가 열릴 때, ``this``도 함께 바인딩이 되는데, 일반적으로 ``this``에는 ``window`` 객체가 바인딩 됩니다.

<br/>

``this``가 ``window``객체가 아닌 경우는 ``실행 컨텍스트``를 호출하는 방식에 의해 발생 합니다.

* 특정 ``객체의 메서드``로 호출 할 때 ``this``: ``메서드``를 가지고 있는 ``객체``
* 생성자 함수 호출을 위해 ``new`` 키워드 사용 시 ``this``: ``새로 생성될 객체``
* ``apply()``, ``call()``, ``bind()`` 를 사용해 ``this``를 직접 지정할 경우



<br/>

[🔺 Top](#top)

<hr/><br/>



##### 03
## 03. Javascript의 ``Event`` 동작방식

Javascript의 ``Event``는 ``3단계``로 동작합니다.

1. ``Capturing Phase``
2. ``Target Phase``
3. ``Bubbling Phase``

<br/>

``click`` 이벤트 발생을 예시로 하겠습니다.

먼저 사용자가 ``click``을 하면, ``DOM`` 요소에서 시작하여, ``click`` 이벤트가 발생한 ``Element``까지 트리를 따라 탐색을 합니다.

이 단계를 ``Capturing Phase`` 라고 합니다.

<br/>

만약 ``click`` 대상 ``Element``를 찾았다면, ``Target Phase``가 되됩니다.

<br/>

``Target Phase`` 다음에는 다시 ``DOM`` 요소까지 트리를 되돌아 가는데, 이 단계를 ``Bubling Phase`` 라고 합니다.

<br/>

``Javascript`` 이벤트의 기본설정은 ``Bubbling`` 단계에서 ``Event Linstener``가 동작하게 됩니다.

즉, 이벤트 발생 지점에 도착한 후, ``Event Listener``가 동작하는 방식 입니다.

중요한 점은 ``Target Phase``에서 ``Event Listener``가 동작한 후, ``Bubbling Phase`` 단계에서 ``click`` 이벤트가 있는 모든 요소에서 ``Event Listener``가 동작한다는 것입니다.

이러한 동작방식에 따라, 다음과 같은 ``Event 설정``을 할 수 있습니다.

* 이벤트 방식: ``Bubbling(기본값)`` 또는 ``Capturing``
* 이벤트 전파 유무: ``stopPropagation``

<br/>

``Javascript``의 이벤트 기본 동작방식이 ``Bubbling``인 이유는, 이벤트가 발생한 대상이 해당 이벤트를 처리하는 것이 가장 적합한 동작이기 때문이고, ``Bubbling Phase``에서 상위 요소의 ``Event Listener``가 동작되어야 ``기능의 확장``을 할 수 있기 때문입니다.

이러한 이유로, 특별한 경우가 아니면 ``Javascript``의 ``Event``는 ``Bubbling``동작에 ``Propagation``방식을 사용합니다.

<br/>

추가로, ``Capturing`` 방식으로 이벤트를 설정하려면, 다음과 같이 작성할 수 있습니다.

```typescript
function myListener(event: MouseEvent): void {
  console.log("클릭 이벤트 발생");
}

const myElement = document.querySelector(".myElement") as HTMLButtonElement;
myElement.addEventListener("click", myListener, true);
```



<br/>

[🔺 Top](#top)

<hr/><br/>



##### 04
## 04. Javascript 비동기 처리

``싱글 스레트``로 동작하는 Javascript는 ``동기식`` 동작을 합니다.

즉, 하나하나 순서대로 처리하는 방식 입니다.

<br/>

하지만, 사용자에 의한 동작(예: ``click``)이나 서버요청에 대한 응답은 비동기 동작 입니다.

``Javascript``에서 비동기 처리를 위해서는 ``Callback``함수를 호출하는 방식으로 처리할 수 있습니다.

``Callback``함수를 사용한 비동기 처리는 ``Callback Hell``이라는 최악의 가독성을 만들 수 있기 때문에, ``ECMA2017``에서 ``Promise`` 객체와 ``async/await``기능이 추가 되었습니다.

<br/>

``async``로 선언된 함수, 메서드는 ``비동기`` 방식으로 처리 되며, 이는 ``Promise``객체(``await 대상``)의 상태값에 따라 마치 ``Callback``이 호출된 것 처럼 다음 코드가 실행 됩니다.



<br/>

[🔺 Top](#top)

<hr/><br/>



