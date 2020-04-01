### 이슈
빌드 시, `Backend Internal error: Exception during code generation` 에러가 발생하면서 빌드가 되지 않음

### 원인
해당 이슈에 대한 원인은 다양하겠지만, 본인의 경우에는 다음과 같은 코드에서 에러 발생

```
binding.rvContents.run {
    adapter = object : BaseSimplePagedListAdapter<ITEM, VDB>(
        resource = ...,
        viewModels = ...,
        diffUtil = object : DiffUtil.ItemCallback<ITEM>() {
            ...
        }
    ) {} 
}
```

위와 같이 `run`, `with`, `apply` 등과 같이 

객체를 receiver 로 암시적으로 전달하는 범위 지정 함수를 사용할 때 

익명객체 내에서 익명객체를 사용하는 경우 문제 발생

---

범위 지정 함수는 inline 으로 정의되어 있는데

inline 함수 안에서 익명객체 내에서 익명객체를 사용하면, scope 처리를 하는 데 문제가 되는 것으로 보임

### 대책
익명객체 내에 익명객체를 사용하는 경우에는 범위 지정 함수 내에서 사용하지 않도록 변경
