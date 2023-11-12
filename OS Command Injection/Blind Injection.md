# Detecting blind OS command injection using time delays

We can use an injected command to trigger a time delay, 
enabling you to confirm that the command was executed based on the time that the application takes to respond
```bash
& ping -c 10 127.0.0.1 &
```
# Example Lab
1) Use Burp Suite to intercept and modify the request that submits feedback.
2) Modify the `email` parameter, changing it to:<br>`email=x||ping+-c+10+127.0.0.1||`
3) Observe that the response takes 10 seconds to return.

## Explanation from you tube
https://youtu.be/YHQXfPWo1vI
