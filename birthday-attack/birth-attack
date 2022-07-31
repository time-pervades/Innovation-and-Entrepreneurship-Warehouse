import random
import string
import math
import sm3


#集合方式生成n个随机数
def getrandomlist(n):
    items=[]
    while len(items)<n:
        tem=random.randint(0,pow（2,64）)
        if tem not in items:
            items.append(tem)
    return items

def birthattack():
    list1_value=[]
    list2_value=[]
    list1_=getrandomlist(pow(2,16))#随机生成满足生日攻击下限个数的明文
    list2_=getrandomlist(pow(2,16))
    for index in range(pow(2,16)):
        value1=sm3.sm3(list1_[index])#遍历每个明文进行加密，并去除前标加入集合
        temp1=hex(value1)[2:]
        t1=temp1[:8]
        list1_value.append(t1)
        value2=sm3.sm3(list2_[index])
        temp2=hex(value2)[2:]
        t2=temp2[:8]
        list2_value.append(t2)
    coincide=set(list1_value)&set(list2_value)#求出两个集合的合集
    #print(cincide)
    if not coincide:
        print("攻击失败！")
        
    else:
        print("攻击成功！")
