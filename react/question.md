## 프로퍼티 A, B, C 순서대로 객체를 네스팅하고 있다면, C 내의 특정 값이 바뀔 때 A와 B도 새로운 객체를 생성해야할까?

```javascript
const [example, setExample] = useState({
  G: 0,
  A: {
    F: 1,
    B: {
      E: 2,
      C: { value: 3 },
    },
  },
});

// 1.
newExample = {
  ...example,
  A: {
    ...example.A,
    B: {
      ...example.A.B,
      C: {
        ...example.A.B.C
        value: 4,
      },
    },
  },
};

// 2.
newExample = {...example}
newExample['A']['B']['C']['value'] = 4
```

1번이 예측가능하기 때문에 안전하다.
예를들면 C에 대해서 React.memo를 사용하고 있는 경우, 참조가 바뀌지 않기 때문에 리렌더링이 발생하지 않는 이슈가 존재한다.
