# SelectKey 주의사항

오늘 대충 이런 일이 있었다. 어떤 값을 Insert하고 그 Key값을 바로 가져오려고 했다.

```xml
<insert id="bbb" parameterType="aaa">
    INSERT INTO abc
    (
        
    )
    VALUES
    (
    )
    <selectKey keyProperty="ddd" resultType="ccc">
        select LAST_INSERT_ID()
    </selectKey>
</insert> 
```

분명히 selectKey에서 ccc(VO)로 매핑을 해 주었는데도 불구하고 에러가 parameterType과 관련된 에러가 발생하였다.

select 구문의 경우 resultType에 명시된 VO에 자동으로 매핑해주는 것을 생각하고 resultType에 VO를 명시했었다.

근데 aaa라는 VO에 ddd의 setter를 찾을 수 없다는 에러 메시지가 발생하여 혼란이 생겼었다.

결국 해결법을 찾긴 했는데 내가 내내 insert에 대해 잘못생각하고 있었다. 

insert는 반환값이 없다 <- 이 부분에 대해 selectKey에서 resultType이 있으니 반환값이 있겠지, 라고 생각했던 것이다.

insert는 반환값이 없고 selectKey를 통해 keyProperty에서 명시한 값은 parameterType에 집어 넣어진다.

결국 return이 아닌 setter로 집어넣는 것이다.

에러 메시지를 좀 더 잘 파악 했었어야 됐는데 이게 왜 리턴이 안되지? 라는 생각밖에 못했던 것 같다.
