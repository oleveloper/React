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

### validateDOMNesting(...): `<p>` cannot appear as a descendant of `<p>`.
```
Warning: validateDOMNesting(...): <p> cannot appear as a descendant of <p>.
```
  
### The prop `xs` of `Grid` must be used on `item`
```
index.js:1 Warning: Failed prop type: The prop `xs` of `Grid` must be used on `item`
```
원인
* Grid의 xs property는 item을 써야하는데, 쓰지 않은 부분이 있었다.

해결
* item={true}를 xs를 사용하는 모든 Grid에 추가해주었다. 


### Use the `defaultValue` or `value` props on select instead of setting `selected` on option.
```
index.js:1 Warning: Use the `defaultValue` or `value` props on <select> instead of setting `selected` on <option>.
```
원인
* defaultValue 또는 value property를 option tag의 selected 대신에 사용하라는 warning message.

해결
* 본 에러는 ag-grid 테이블을 사용하면서 pagination 을 구현한 부분에 발생한 warning으로
  pagination 은 아래와 같이 구현되어 있었다.
```javascript
<select onChange={onPageSizeChanged} id="page-size">
    <option value="25" selected={pageSize == "25"}>
      25
    </option>
    <option value="100" selected={pageSize == "100"}>
      100
    </option>
    <option value="500" selected={pageSize == "500"}>
      500
    </option>
    <option
      value={rowNum}
      selected={
        pageSize != "25" && pageSize != "100" && pageSize != "500"
      }
    >
      All
    </option>
</select> 
```
상기 코드에서 selected property를 삭제하여 메시지 발생하지 않도록 하였으며 잘 동작하는지 테스트까지 완료하였다.

