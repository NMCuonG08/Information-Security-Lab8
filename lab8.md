```bash
docker exec -it outsider-10.9.0.5 sh -l
```

![image](https://github.com/user-attachments/assets/3d745998-9eaa-4db1-bfd2-b6701c03934e)


![image](https://github.com/user-attachments/assets/b2e4ce78-a562-477e-bab1-807bd521ab9f)

![image](https://github.com/user-attachments/assets/95ebce57-edeb-4640-a255-d3e478427f3d)

![image](https://github.com/user-attachments/assets/3fc335b2-8268-4048-9c32-1cc88c160057)


Ping OK ![image](https://github.com/user-attachments/assets/3d9543a7-f1c5-4291-99d5-236c1143c854)

  ![image](https://github.com/user-attachments/assets/3a01843e-4a82-4d65-b4e9-dd57a795bd04)

![image](https://github.com/user-attachments/assets/8bd09f2d-9c72-4582-b169-98b387cbd619)


ex1. 

## block all access

```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```


![image](https://github.com/user-attachments/assets/3341fbe8-d899-46ec-8fe6-c638206b0a88)

=>  ping success 

![image](https://github.com/user-attachments/assets/ba569dc8-7129-4189-8b45-9b56da956078)

![image](https://github.com/user-attachments/assets/7b06b6eb-5643-49ec-ba51-7ee936b26eb0)

=> ping failed

![image](https://github.com/user-attachments/assets/bdac9bee-615f-4c96-baa7-755497aed300)

![image](https://github.com/user-attachments/assets/9dcc06ca-34e2-4db1-8a78-1920255a2783)

=>  ping success  again

![image](https://github.com/user-attachments/assets/a2b46acf-a0e5-49cf-a2df-a6f0aa1a8e27)


Task 1b:


![image](https://github.com/user-attachments/assets/588377ff-c91c-4c2b-83e7-cda47f6cbee5)


```bash
 iptables -A FORWARD -s 10.9.0.0/24 -d 172.16.10.110 -j DROP
```

![image](https://github.com/user-attachments/assets/a3afa7c7-eb72-4d77-964a-b95a1e846bee)


![image](https://github.com/user-attachments/assets/21eaf4a2-0507-4228-b9ab-99a785192823)

Task 1c:


Test 

![image](https://github.com/user-attachments/assets/8df55463-5588-42ac-8749-f679c32d3bc1)


```bash
iptables -A FORWARD -s 172.16.10.0/24 -d 10.9.0.10 -j DROP
```

![image](https://github.com/user-attachments/assets/0779e69a-623f-44d5-874d-d91fe7f05bcc)

stop computers on subnet 172.16.10.0/24 from accessing the badsite.
















