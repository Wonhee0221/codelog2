# Dynamic programming 문제풀이
## 문제 1
![image](https://user-images.githubusercontent.com/91041488/142754210-f6dd4fc4-487e-45ba-9f0e-045c4aa9c12d.png)  

<풀이>
```python
n=int(input())

dp=[0 for _ in range(n+1)]
dp[1]=1

for i in range(2,n+1):
    dp[i] = dp[i-1]+dp[i-2]
    
print(dp[n])
```

## 문제 2 
![image](https://user-images.githubusercontent.com/91041488/142754378-483dc985-9d23-4d2c-8f36-a0bf4082a9d3.png)    
<풀이>  
```python
n=int(input())

dp=[0 for _ in range(n+1)]

for i in range(2,n+1):
    dp[i]= dp[i-1] + 1
    if i % 3 ==0:
        dp= min(dp[i//3]+1, dp[i])
    elif i % 2 ==0:
        dp= min(dp[i//2]+1, dp[i])

print(dp[n])
```

## 문제 3  
![image](https://user-images.githubusercontent.com/91041488/142754730-7440bed2-e108-46bd-9bb0-467a8dab7d40.png)  

<풀이>  
```python
t=int(input())
n=[]
max=11

dp=[1 for _ in range(max+1)]
dp[2]=2
dp[4]=4

for i in range(4,max):
    dp[i]= dp[i-1] + dp[i-2] + dp[i-3]
    
for  i in range(t):
    n=int(int(input())
    
print(dp[n])
```
