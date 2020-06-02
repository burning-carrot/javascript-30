# CSS JS Clock

음.. 간단하지만 어렵네요. 영상 마지막에 transition 을 잠깐 없애던지 degree 를 계속 세라고 하길래 ~~transition 을 잠깐 없애면 또 0초로 돌아갈때만 초침이 순간이동 할 것 같아서 저는 그냥 degree 를 계속 중첩해서 셌습니다. degree 가 억단위가 넘어가면 이상하게 움직이긴 하는데 현재로서는 딱히 방법이 떠오르지 않네요 ㅎ;;~~

일단, 시, 분, 초가 `90deg` 인 경우 `450deg` 로 바꿔쳤습니다. `transitionend` 이벤트 리스너에서 트랜지션이 끝난 이후 `e.target.style.transform` 이 `450deg` 라면 `transition` 을 없앤 후 `90deg` 로 돌려놨습니다.

```javascript
if (curDeg === 450) {
  e.target.style.transition = "none";
  e.target.style.transform = "rotate(90deg)";
}

// settimout 안걸고 바로 transition 을 복구시키면 rotate 하는 와중에 트랜지션이 적용되는 ?? 그래서 트랜지션 먹은 상태로 바늘이 이동하길래 이렇게 해놨습니다.
setTimeout(() => {
  e.target.style.transition = "all 0.3s";
}, 0);
```

매 초마다, 매 분마다 매 시간마다 만 해당 초, 분, 시 를 업데이트하기 위해서 함수를 3개로 쪼갰습니다. (setDate에 같이 있으면 매 초마다 같은 분, 시를 업데이트 하니까 낭비라고 생각했습니다.)
