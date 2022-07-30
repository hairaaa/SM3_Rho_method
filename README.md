# SM3_Rho_method
SM3与Rho method:

简化操作，初始时对512bit长度的串进行杂凑，比对杂凑值前16bit，256次内可容易找到。
![image](https://user-images.githubusercontent.com/104775629/181994693-7e929700-2258-445d-9088-27cc9fabe663.png)


#随机生成两个长度为128x4bit的数据进行生日攻击使得两串数据在进行了sm3之后杂凑值相同

def Rhomethod():

    #在此只进行简单的操作，比对杂凑值的前16bit
    
    # 初始化一个列表,不停存入杂凑值的前16bit
    
    list_r = []
    
    message = random_hex(128)
    
    for i in range(256):
    
        # 计算出杂凑值
        
        m = Fill(message)  # 填充后消息
        
        M= Group(m)  # 数据分组
        
        Vn = Iterate(M)
        
        result = ''
        
        for x in Vn:
        
            result += (hex(x)[2:])
            
        print(result[:4])
        
        message=result
        
        if (result[:4]in list_r):
        
            print("成功找到！")
            
            print("其杂凑值前16bit为",result[:4])
            
            return 1
            
        else:
        
            list_r.append(result[:4])
            

