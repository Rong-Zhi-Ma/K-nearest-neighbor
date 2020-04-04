＃<center>欢迎来到我的GitHub个人主页</center>
<br/>这里是我的第一个Python算法实战项目：KNN算法
<br/>
'''
#-*- coding: utf-8 -*-
#K-NN算法的回归实战
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei']
plt.rcParams['axes.unicode_minus']=False 

def distance(x):
    Q=int(x//0.2) #取商quotient
    C=x%0.2 #取余remainder
    if Q<=2:
        dis_x_data=x_data[0:Q+4]
        data_y_data=y_data[:,0:Q+4]
    elif Q>=48:
        if C!=0:
            dis_x_data=x_data[Q-2:50]
            data_y_data=y_data[:,Q-2:50]
        else:
            dis_x_data=x_data[Q-3:51]
            data_y_data=y_data[:,Q-3:50]
    else:
        if C!=0:
            dis_x_data=x_data[Q-2:Q+4]
            data_y_data=y_data[:,Q-2:Q+4]
        else:
            dis_x_data=x_data[Q-3:Q+4]
            data_y_data=y_data[:,Q-3:Q+4]
    w=1/(np.square(dis_x_data-x)+0.02) #引入偏置防止数据点与测试点重合引起的报错
    mean_=np.sum(w*data_y_data,axis=None)/np.sum(w,axis=None)
    return mean_
                
x_data=np.linspace(0,10,num=51) 
#创建标准标准正态分布形式噪声
random_data=np.random.randn(1,51) 
#对y=20*sin(x_data)引入噪声
y_data=20*np.sin(x_data)+random_data
plt.plot(x_data,y_data.T,'r+')

#创建测试点
x_=np.linspace(0,10,num=91)
num_1=0
num_2=0
y_P=[]
x_data_test=[]
for i in x_:
    y_P.insert(num_1,distance(i))
    num_1=num_1+1
for j in x_data:
    x_data_test.insert(num_2,distance(j))
    num_2=num_2+1
train_err=np.sum(np.abs(y_data-x_data_test),axis=None)/np.sum(np.abs(y_data),axis=None)
test_err=np.sum(np.abs(20*np.sin(x_)-y_P),axis=None)/np.sum(np.abs(20*np.sin(x_)),axis=None)
plt.plot(x_,y_P,'b-') 
plt.title('K=6时回归曲线\n训练误差为： '+str(train_err)+'\n测试误差为： '+str(test_err))
y_target=20*np.sin(x_) 
plt.plot(x_,y_target,'y-')
plt.show()
'''
<br/><br/>
本次修改时间：2020年4月4日
