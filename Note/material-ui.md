### The key `heading` provided to the classes prop is not implemented in ForwardRef(Accordion)
```
index.js:1 Material-UI: The key `heading` provided to the classes prop is not implemented in ForwardRef(Accordion).
You can only override one of the following: root,rounded,expanded,disabled.
```
원인 
* heading이라는 key는 Accordion의 ForwardRef에서 구현되지 않으며 root, rounded, expanded, disabled 중 하나를 override해서 사용할 수 있다는 에러.
아래와 같이 사용한 것이 문제가 됨.

```javascript
const Accordion = withStyles({
    root: {
        width: '100%',
        border: 'transparent',
        boxShadow: 'none',
        display: 'inline',
    },
    heading: {
        fontSize: 14,
        fontWeight: 'bold',
        color: '#00A4C3',
        height: 'fit-content'
    },
  })(MuiAccordion);
```
해결
* guide message대로 root, rounded, expanded, disabled 중 하나를 override해서 사용하려고 하였으나 heading을 사용하지 않고 있어 삭제하였다. 
