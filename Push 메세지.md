# PUSH

```
PushRequestVo vo = new PushRequestVo();  
  
List<String> toUsers = new ArrayList<String>();  
toUsers.add("eylee");  
  
vo.setAppName("SFATABLET");  
vo.setTrxType("INSTANT");  
vo.setToAll(false);  
vo.setFromUser("system");  
vo.setToUsers(toUsers);  
vo.setMessageCategory("def");  
vo.setFromUserIp("127.0.0.1");  
vo.setMessageSubject("푸쉬 제목");  
vo.setMessageContent("푸쉬 내용 입니다.");  
  
//화면 연결정보 전달  
vo.setMenuUri("test");  
vo.setMessagePayloadByMenuUri();  
vo.setMessageType("DEF0001");  
  
pushService.fireMessage(vo);
```