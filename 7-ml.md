# 教師付き機械学習(回帰)

## 1次元

```python
import numpy as np
import matplotlib.pyplot as plt

# %matplotlib inline

X_min = 4
X_max = 30

def generate_data():
    np.random.seed(seed=1)
    X_n = 16
    X = 5 + 25 * np.random.rand(X_n)
    Prm_c = [170,108,0.2]
    T = Prm_c[0] - Prm_c[1] * np.exp(-Prm_c[2] * X) + 4 * np.random.randn(X_n)
    print(X)
    np.savez('ch5_data.npz',X=X, X_min=X_min, X_max=X_max ,X_n=X_n ,T=T)# -*- coding: utf-8 -*-
    return X,T

def show_data(X,T):
    plt.figure(figsize=(4,4))
    plt.plot(X,T,marker='o',linestyle='None',markeredgecolor='black',color='cornflowerblue')
    plt.xlim(X_min, X_max)
    plt.grid(True)
    plt.show()

def show_data_and_line(X,T,w):
    plt.figure(figsize=(4,4))
    xb = np.linspace(X_min,X_max,100)
    y = w[0] * xb + w[1]
    plt.plot(xb,y,color=(.5,.5,.5), linewidth=4)
    plt.plot(X,T,marker='o',linestyle='None',markeredgecolor='black',color='cornflowerblue')
    plt.xlim(X_min, X_max)
    plt.grid(True)    
    plt.show()


# 平均二乗誤差
def mse_line(X,T,W):
    Y = W[0] * X + W[1]
    mse = np.mean((Y-T)**2)
    return mse

# 平均二乗誤差の勾配
def dmse_line(X,T,W):
    Y = W[0] * X + W[1]
    d_W = [0,0]
    d_W[0] = 2 * np.mean((Y-T)*X)
    d_W[1] = 2 * np.mean(Y-T)
    return d_W

#　勾配法
def fit_line_num(X,T,w_init):
    alpha = 0.001 #学習率
    eps = 0.1 #繰り返しをやめる絶対値に閾値
    w_i = w_init
    for i in range(1,1000000):
        dmse = dmse_line(X,T,w_i)
        w_i[0] = w_i[0] - alpha * dmse[0]
        w_i[1] = w_i[1] - alpha * dmse[1]
        if max(np.absolute(dmse)) < eps:
            break
    return w_i[0],w_i[1],dmse

X,T = generate_data()
show_data(X,T)


w_init = [10.0, 165,0] #初期化パラメータ
W0,W1,dMSE = fit_line_num(X,T,w_init)

print(W0,W1)

#plt.figure(figsize=(4,4))
W=np.array([W0,W1])
show_data_and_line(X,T,W)
```


# 2次元

```python

X0 = X
X0_min = 5
X0_max = 30
np.random.seed(seed=1)
X1 = 23 * (T/100)**2 + 2 * np.random.random(X_n)
X1_min = 40
X1_max = 75
print(X0)
print(X1)
print(T)

def show_data2(x0,x1,t):
    plt.figure(figsize=(6,5))
    ax = plt.subplot(1,1,1,projection='3d')
    for i in range(len(x0)):
        ax.plot([x0[i],x0[i]],[x1[i],x1[i]],[120,t[i]],color='gray')
        ax.plot(x0,x1,t,'o',color='cornflowerblue',markeredgecolor='black',markersize=6,markeredgewidth=0.5)
        ax.view_init(elev=35,azim=-75)
    plt.show()

def mse_plane(X0,X1,T,W):
    Y = W[0] * X0 + W[1] * X1 + W[2]
    mse = np.mean((Y-T)**2)
    return mse


def dmse_plane(X0,X1,T,W):
    Y = W[0] * X0 + W[1] * X1 + W[2]
    d_W = [0,0,0]
    d_W[0] = 2 * np.mean((Y-T)*X0)
    d_W[1] = 2 * np.mean((Y-T)*X1)
    d_W[2] = 2 * np.mean(Y-T)
    return d_W

#　勾配法
def fit_plane_num(X0,X1,T,w_init):
    alpha = 0.000025 #学習率
    eps = 2.0 #繰り返しをやめる絶対値に閾値
    w_i = w_init
    for i in range(1,1000000):
        dmse = dmse_plane(X0,X1,T,w_i)
        w_i[0] = w_i[0] - alpha * dmse[0]
        w_i[1] = w_i[1] - alpha * dmse[1]
        w_i[2] = w_i[2] - alpha * dmse[2]
        #print(max(np.absolute(dmse)))
        #import time
        #time.sleep(1)
        if max(np.absolute(dmse)) < eps:
            break
    return w_i[0],w_i[1],w_i[2],dmse

def show_data2_and_plane(x0,x1,t,w0,w1,w2):
    plt.figure(figsize=(6,5))
    ax = plt.subplot(1,1,1,projection='3d')
    for i in range(len(x0)):
        ax.plot([x0[i],x0[i]],[x1[i],x1[i]],[120,t[i]],color='gray')
        ax.plot(x0,x1,t,'o',color='cornflowerblue',markeredgecolor='black',markersize=6,markeredgewidth=0.5)
        ax.view_init(elev=35,azim=-75)
    px0 = np.linspace(X0_min,X0_max,5)
    px1 = np.linspace(X1_min,X1_max,5)
    px0,px1 = np.meshgrid(px0,px1)
    y = w0*px0 + w1*px1 + w2
    ax.plot_surface(px0,px1,y,rstride=1,cstride=1,alpha=0.3,color='blue',edgecolor='black')
    plt.show()


show_data2(X0,X1,T)
w_init = [10.0, 44.0,165,0] #初期化パラメータ
W0,W1,W2,dMSE = fit_plane_num(X0,X1,T,w_init)
print(W0,W1,W2)
show_data2_and_plane(X0,X1,T,W0,W1,W2)
```
