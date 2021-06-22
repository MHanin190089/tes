# Integrasi Numerik	

Terdapat 2 jenis integral

1. Integral tertentu merupakan suatu bilangan. Pada integral ini terdapat suatu batasan, yaitu batas atas dan batas bawah.

   contoh: 
   $$
   \int ^{2}_{1}2xdx = x^2 ] ^{2}_{1} = (2)^2 - (1)^2 = 3
   $$

2. Integal tak tentu merupakan suatu fungsi yang berbeda satu sama lain oleh konstanta.

   contoh: 
   $$
   \int 3x^2dx = x^3 + C
   $$

Jadi **Metode integrasi numerik** adalah suatu cara untuk menghitung luas daerah di bawah fungsi yang dimaksud pada selang yang diberikan. Berikut ini adalah metode integrasi numerik yang akan kita bahas:

#### 1. Metode Newton-Cotes

Dalam metode ini, fungsi didekati dengan polynomial tingkat *n*. Jadi untuk menggunakan metode ini, kita harus menggunakan integral dari polynomial.
$$
\int ^{b}_{a} f(x)dx \approx \int ^{b}_{a} (a_{0}+a_{1}x+...+a_{n}x^n)dx
$$

$$
\rightarrow \int ^{b}_{a} f(x)dx \approx a_{0}(b-a)+a_{1}\dfrac{(b^2-a^2)}{2}+...+a_{n}\dfrac{(b^{n+1}-a^{n+1})}{n+1}
$$

​		Terdapat 2 jenis Newton_Cotes:

​		a.	Metode tertutup = batas awal dan akhir disebutkan

​		b.	Metode terbuka = batas integrasi diperbesar di luar garis rentang atau disebut 

​				ekstapoksi.	

Metode ini dibagi menjadi 3. diantaranya:

- ###### Trapesium (trapezoid)

  merupakan salah satu dari metode intgrasi newton tertutup dengan memakai aproksimasi polynomial orde 1 dan menggunakan aturan trapesium.

  => Newton Cotes orde 1
  $$
  I = \int ^{b}_{a} f_{1}(x)dx
  $$
  => Rumus Luas Trapesium
  $$
  L = t\dfrac{(a+b)}{2}
  $$
  => Sehingga ketika digabungkan, akan menjadi seperti berikut ini:
  $$
  I=(b-a)\dfrac{f(a)+f(b)}{2}
  $$
  Rumus tersebut sama dengan rumus luas trapesium dengan sisi atas f(a). sisi bawah f(b) dan tinggi (b-a)

  => Untuk mencari besarnya error yang dihasilkan yaiu menggunakan rumus:
  $$
  \varepsilon_{a} = -\dfrac{1}{12}\overline{f"}(b-a)^3
  $$

  

  $$
  \overline{f"}
  $$
  merupakan nilai rata2 dari turunan kedua yang dirumuskan seerti dibawah ini:
  $$
  \overline{f"}=\dfrac{\int ^{b}_{a}f"(x)}{b-a}
  $$
  Algoritma untuk metode trapezoid:

  a.	 Memilih suatu fungsi yang akan diintegrasi

  b.	 Tentukan batas atas (a) dan batas bawah (b)

  c.	 Hitung lebar segmen dengan rumus 
  $$
  h = \dfrac{b-a}{N}
  $$
  ​			N = jumlah segmen

  d.	Berikan pada fungsi yang akan diintegrasi 
  $$
  I = f(a)+f(b)
  $$
  e.	Kemudian hitung *I* untuk *n = I* sampai *n = N - I*

  f.	 Cetak hasilnya

  **Source Code**

  program  untuk melakukan pendekatan hasil dari 
  $$
  \int^{2}_{1}(x^2+2x+1)dx
  $$

```python
f = inline ('x^2 + 2*x+1','x')

hsl_error = 1,6667

a= input("batas atas : ")

b = input("batas bawah : ")

N = input("jumlah segmen : ")

h = (a - b) / N

sum = f(a) + f(b)

fak = 2

for i in range (1, N-1):
    x = a +i * h
    sum = sum  + 2 * f(x)

hasil = sum * h /2

selisih = hsl_error - hasil

error = abs( selisih / hsl_error)

print(hasil)

print(error)
```

- ###### **Simpson 1/3**

merupakan suatu metode yang akan digunakan dalam menghitung luas suatu kurva polinomial derajat dua [P2(x)] atau berderajat tiga [P3(x)] dengan menggunakan pendekatan partisi berbentuk parabola.

Aturan ini membagi / mempartisi kurva polinom derajat dua dengan 3, 5, 7 titik, dan seterusnya (berkelipatan 2).

=> Berikut rumus dari metode integrasi numerik dengan menggunakan aturan Simpson 1/3
$$
\dfrac{b-a}{3}(f_{0}+4f_{1}+f_{2})
$$
=> sedangkan untuk mencari estimasi kesalahan (error), maka:
$$
-\dfrac{1}{90}f^{4}(b-a)^5
$$
Algoritma untuk metode Simpson 1/3

a.	Mendefinisikan suatu fungsi yg ingin diintegrasi

b.	Menentukan batas atas (a) dan batas bawah (b)

c.	Tentukan jumlah segmen / bagian (N)

d.	Menghitung lebar segmen dengan rumus seperti sebelumnya
$$
\dfrac{b-a}{N}
$$
e.	Tentukan  jumlahan 
$$
sum = f(a)+f(b)
$$
f.	Tentukan faktor bobot 
$$
fak = 4
$$
g.	Hitung jumlahan dari *i* = 1 sampai *i* = *N* - 1

 - Menentukan node dari tiap - tiap 
   $$
   x_{i}= a + i h
   $$

 - Berilah suatu syarat jika (*fak* = 4), maka *fak* = 2

 - Hitunglah nilai integral 
   $$
   sum = sum + fak*f(x)
   $$



h.	Hitunglah hasil akhirnya 
$$
Hasil= \dfrac{h}{3} sum
$$
**Source Code** (matlab)

```python
f = inline ('exp(x)', 'x')

a = input("batas atas : ")

b = input("batas bawah : ")

N = input("jumlah segmen : ")

kira = f(a) - f(b)

if (mod(N, 2) != 0)

​		N = N+1

h = (a - b) / N

sum = f(a) + f(b)

fak = 2

for i in range (1, N-1):
    x = a +i * h
    if (fak == 2):
        fak = 4
    else:
        fak = 2;
	sum = sum  + fak * f(x)

hasil = h /3 * sum

error = abs( kira -  hasil)

print(hasil)

print(error)
```

- ###### **Simpson 3/8**

metode ini hampir sama dengan metode sebelumnya, hanya saja ini digunakan untuk meningkatkan ketelitian yang telah ada pada metode Simpson 3/8. Metode ini mensyaratkan jumlah langkah dengan kelipatan 3.

Metode  Simpson 3/8 untuk 3 segmen dinyatakan dengan rumus sebagai berikut
$$
\dfrac {3(b-a)}{8}(f_{0}+4f_{1}+3f_{2}+f_{3})
$$
dan jika banyak segmen, menggunakan rumus: 
$$
\int^{x_{0}+Nh}_{x_{0}}f(x)dx = \dfrac{3h}{8}[f(x_{0})+3f(x_{1})+3f(x_{2})+2f(x_{3})+3f(x_{4})+3f(x_{5})+2f(x_{6})+...+2f(x_{N-3})+3f(x_{N-2})+3f(x_{N-1})+f(x_{0}+Nh)]
$$
​			N = Jumlah segmen

​			h = (b - a) / N

Algoritma untuk metode Simpson 3/8, sebagai berikut:

 - Mendefinisikan fungsi yang ingin diintegrasi

 - Menentukan batas atas (a) dan batas bawah (b)

 - Menentukan jumlah segmen (N) => harus berkelipatan 3

 - Menghitung lebah segmen dengan rumus
   $$
   h = \dfrac{b-a}{N}
   $$

 - Tentukan  jumlahan 
   $$
   sum = f(a)+f(b)
   $$

 - Hitung jumlahan dari *i* = 1 sampai *i* = *N* - 1
   $$
   x=a+i*h
   $$

   - if (mod (i, 3) = 1 or mod (i, 3) =2), maka

     *fak* = 3

   - else, maka *fak* = 2

 - Hitunglah nilai integral 
   $$
   sum = sum + fak*f(x)
   $$


   Jadi, Hasilnya
$$
   Hasil = \dfrac{3h}{8}sum
$$

**Source Code **(Matlab)

```python
f = inline (' x**2+1', 'x')

fd = inline ('2x^2 + 3x**3', 'x')

a = input("batas atas : ")

b = input("batas bawah : ")

N = input("jumlah segmen (minimal 3) : ")

kira = fd(a) - fd(b);

h = (a - b) / N;

sum = f(a) + f(b)

for i in range (1, N-1):
    x = a +i * h
    if (mod(i, 3) == 2 || mod(i, 3) == 1):
        fak = 3
    else:
        fak = 2
    sum = sum  + fak * f(x)

hasil = (3 *h)/8 * sum

error = abs( kira -  hasil)

print(hasil)

print(error)
```



# **Persamaan Diferensial Biasa**

**Persamaan diferensial** merupakan persamaan yang mengandung turunan dari variabel terikat dan bebarapa variabel bebas. Sedangkan **persamaan diferensial biasa** adalah persamaan diferensial dimana fungsi yang tak diketahui (varibel terikat) merupakan fungsi dari variabel bebas tunggal.



1. #### **Bentuk Umum**

   Terdapat dua bentuk umum dari persamaan diferensial, yaitu:

   a.	Bentuk Implisit
   $$
   F(x, y, y') = 0
   $$
   b.	Bentuk Eksplisit
   $$
   y' = f(x, y)
   $$
   ​	Turunan dari sebuah variabel dapat diganti dengan tanda petik. Contoh:
   $$
   y' = \dfrac{dy}{dx}
   $$

   $$
   y'' = \dfrac{d^2y}{dx^2}
   $$

   

2. #### **Orde Persamaan Diferensial** 

   Orde  dalam persamaan diferensial ditentukan berdasarkan turunan tertinggi dalam persamaan yang dibuat.

   - Orde pertama

   $$
   y' = \cos x
   $$

   - Orde kedua

   $$
   y'' + 9y = e^{-2x}
   $$

3. #### **Metode Penyelesaian Persamaan Diferensial**

   Berikut ini bebearapa metode yang dapat digunakan untuk menyelesaikan persamaan diferensial biasa:

- ###### Metode Deret Taylor

  Beberapa orde dalam deret taylor:

  1. Deret taylor orde 0
     $$
     f(x_{i+1})=f(x_{i})
     $$

  2. Deret taylor orde 1
     $$
     f(x_{i+1})=f(x_{i})+f'(x_{i})\dfrac{\Delta x}{1!}
     $$

  3. Deret taylor orde 2
     $$
     f(x_{i+1})=f(x_{i})+f'(x_{i})\dfrac{\Delta x}{1!}+f''(x_{i})\dfrac{\Delta x^2}{2!}
     $$

  4. dst

  Berikut persamaan dari deret taylor:
  $$
  f(x_{i}+1)=f(x_{i})+f'(x_{i})\dfrac{x_{i+1}-x_{i}}{1!}+f''(x_{i})\dfrac{(x_{i+1}-x_{i})^2}{2!}+...+f^{(n)}(x_{i})\dfrac{x_{i+1}-x_{i}}{n!}+Rn
  $$
  ket:

  f',  f'', ... = turunan pertama, turunan kedua, ... dst.

  Rn = Kesalahan pemotongan (error)

  

  **Algortima untuk metode deret taylor:**

  - Menentukan jumlah iterasi dan jarak partisi
  - Menentukan x0 dan y0
  - Menentukan turunan yang diperlukan 
  - Cetak hasil

  **Source Code** (Matlab)

  ```
  y1=inline (‘sin(2*x) +2*y’);
  y2=inline(‘2*cos(2*x) + 2 * sin (2*x) + 4*y ‘);
  y3=inline (‘4*cos(2*x) + 8*y’);
  y4=inline (’16*y’);
  y0=0;
  x0=1;
  h=0.1;
  n=10;
  for i = 1:n;
      x(i)=x0 +i*h;
      y(i)= y0 + (x(i)-x0)*y1(x0,y0) + (x(i)-x0)^2*y2(x0,y0)/factorial(2) + (x(i)-x0)^3*y3(x0,y0)/factorial(3)+ (x(i)-x0)^4*y4(y0)/factorial(4);
      disp(sprintf(‘|%3g |%5.3f |%8.6f |’,i,x(i),y(i)));
  end
  plot(x,y)
  ```

  **Output**

  ```
  |  1 |1.100 |0.095584 |
  |  2 |1.200 |0.199366 |
  |  3 |1.300 |0.309682 |
  |  4 |1.400 |0.424867 |
  |  5 |1.500 |0.543257 |
  |  6 |1.600 |0.663188 |
  |  7 |1.700 |0.782993 |
  |  8 |1.800 |0.901010 |
  |  9 |1.900 |1.015572 |
  | 10 |2.000 |1.125017 |
  ```

  

- ###### Metode Euler

  merupakan metode orde pertama untuk meneyelesaikan persamaan diferensial biasa dengan nilai awal yang telah diberikan. Penyelesaian dengan metode ini yaitu mencari nilai fungsi y(x) pada titik x tertentu dari persamaan diferensial biasa f( x, y).

  Dengan menggunakan turunan numerik, maka rumusnya:
  $$
  f'(x,y)= \dfrac{f(x+h,y)-f(x,y)}{h}+O(h)
  $$
  Substitusikan waktu t dan besaran y ke rumus sebelumnya, maka ditemukan rumus:
  $$
  f'(t,y)= \dfrac{f(t+h,y)-f(t,y)}{h}+O(h)
  $$
  atau bisa juga menjadi
  $$
  f(t+h,y)=f(t,y)+hf'(t,y)+O(h)
  $$
  Sehingga persamaan diferensial biasa dapat diselesaikan melalui iterasi, yang mana:
  $$
  y0=y(a)=a
  $$

  $$
  f_{i+1}=f_{i}+hf(t_{i},y) 
  $$

  untuk i = 0, 1, 2, 3, ... , n - 1
  $$
  h= \dfrac{(b-a)}{n}
  $$

  $$
  t_{i}=a+ih
  $$

  Algortima untuk metode euler, sebagai berikut:

  - Mendefinisikan fungsi f(x, y)
  - Menentukan titik awal x0 dan y0
  - Meneentukan nilai h
  - Menentukan jumlah iterasi n 
  - Substitusikan ke dalam rumus 

  **Source Code** (Python)

  ```
  # fungsi
  def f(x,y):
      return x+y
  
  # atau
  # f = lambda x: x+y
  
  # fungsi metode euler
  def euler(x0,y0,xn,n):
      
      # Calculating step size
      h = (xn-x0)/n
      
      print('\n-----------Solusi-------------')
      print('------------------------------')    
      print('x0\ty0\tslope\tyn')
      print('------------------------------')
      for i in range(n):
          slope = f(x0, y0)
          yn = y0 + h * slope
          print('%.4f\t%.4f\t%0.4f\t%.4f'% (x0,y0,slope,yn) )
          print('------------------------------')
          y0 = yn
          x0 = x0+h
      
      print('\nAt x=%.4f, y=%.4f' %(xn,yn))
  
  # input x0 dan y0
  print('Masukkan nilai awal:')
  x0 = float(input('x0 = '))
  y0 = float(input('y0 = '))
  
  print('Enter calculation point: ')
  xn = float(input('xn = '))
  
  print('Masukkan jumlah iterasi:')
  step = int(input('Jumlah iterasi = '))
  
  # Panggil metode euler
  euler(x0,y0,xn,step)
  ```

   Output

  ```
  Masukkan kondisi awal:
  x0 = 0
  y0 = 1
  Enter calculation point: 
  xn = 1
  Masukkan jumlah iterasi:
  Jumlah iterasi = 10
  
  -----------Solusi-------------
  ------------------------------
  x0	y0	slope	yn
  ------------------------------
  0.0000	1.0000	1.0000	1.1000
  ------------------------------
  0.1000	1.1000	1.2000	1.2200
  ------------------------------
  0.2000	1.2200	1.4200	1.3620
  ------------------------------
  0.3000	1.3620	1.6620	1.5282
  ------------------------------
  0.4000	1.5282	1.9282	1.7210
  ------------------------------
  0.5000	1.7210	2.2210	1.9431
  ------------------------------
  0.6000	1.9431	2.5431	2.1974
  ------------------------------
  0.7000	2.1974	2.8974	2.4872
  ------------------------------
  0.8000	2.4872	3.2872	2.8159
  ------------------------------
  0.9000	2.8159	3.7159	3.1875
  ------------------------------
  
  At x=1.0000, y=3.1875
  ```

# **Sistem Persamaan Aljabar Linear**

**Persamaan linear ** adalah sebuah persamaan, dimana setiap sukunya memiliki konstanta.
$$
a_{1}x_{1}+a_{2}x_{2}+...+a_{n}x_{n} = b
$$
**Sistem persamaan linear** adalah himpunan dari persamaan linear yang terdiri dari beberapa variabel.

Berikut ini metode yang dapat digunakan untuk menyelesaikan sistem persamaan linear:

- Metode Eliminasi Gauss 

  

- Metode Jacobi

  merupakan metode yang konvergen, itu membuat setiap persamaan harus diubah sedemikian hingga koefisien dari nilai mutlak harus memiliki nilai paling besar satu.
  $$
  \left|\dfrac{a_{ij}}{a_{ii}}\right|\leq 1
  $$
  Metode Iterasi Jacobi disebut sebagai salah satu metode tak langsung, karena berawal dari suatu hampiran penyelesaian awal dan kemudian berusaha memperbaiki hampiran dalam tak berhingga namun langkah konvergen.

  

  Metode Jacobi memiliki rumus sebagai berikut:
  $$
  x_{i}=\dfrac{b_{i}-\Sigma_{i\neq j}a_{ij}x_{j}}{a_{ii}}
  $$
  atau
  $$
  x_{1}^1=\dfrac{(b_{1}-a_{12}x_{2}^0-a_{13}x_{3}^0)}{a_{11}}
  $$

  $$
  x_{2}^1=\dfrac{(b_{2}-a_{21}x_{1}^0-a_{23}x_{3}^0)}{a_{22}}
  $$

  $$
  x_{3}^1=\dfrac{(b_{3}-a_{31}x_{1}^0-a_{32}x_{2}^0)}{a_{33}}
  $$

  

  akan berakhir jika
  $$
  x_{1}^{n-1}\approx x_{1}^n, x_{2}^{n-1}\approx x_{2}^n, x_{3}^{n-1}\approx x_{3}^n
  $$
  **Algoritma untuk metode iterasi Jacobi:**

  - Menentukan persamaan linear yang akan dikerjakan
  - Membuat bentuk matrik
  - Menentukan nilai awal dari Xi (i=1, 2, ..., n)
  - Substitusikan nilai awal Xi pada rumus seperti di atas.
  - Untuk setiap nilai Xi jika telah diketahui maka subtsitusikan  

  **Source Code** (Python)

  ```
  mtrk=[
      [[11,-1,2,0,2,1,1,1,2,3],["X1"],[14]],
      [[-1,11,-1,3,1,2,2,2,1,1],["X2"],[25]],
      [[2,-1,10,-1,0,1,-2,1,3,3],["X3"],[2]],
      [[0,3,-1,8,1,0,2,-1,2,2],["X4"],[17]],
      [[1,2,0,1,2,-1,0,1,-3,4],["X5"],[8]],
      [[1,2,0,1,2,2,2,2,2,1],["X6"],[9]],
      [[1,2,0,1,2,2,3,0,1,-2],["X7"],[0]],
      [[1,2,0,1,2,2,3,2,0,-1],["X8"],[1]],
      [[1,2,0,1,2,2,3,2,-2,0],["X9"],[-2]],
      [[1,2,0,1,2,2,3,2,-2,-2],["X10"],[-4]],
  ]
  for i in range(len(mtrk[0][0])):
      mtrk[i][1][0]=0
  K1=[]
  for k in range(10):
      for i in range(len(mtrk)):
          # print(k,i)
          Xi=mtrk[i][1][0]
          # print("Xi = ",Xi)
          sum=mtrk[i][2][0]
          # print("sum = ",sum)
          for j in range(len(mtrk)):
              if i == j :
                  continue
              sum=sum-mtrk[i][0][j]*mtrk[j][1][0]
                  # print(f"mtrk[i][0][j] ={mtrk[i][0][j]} mtrk[i][1][0] = {mtrk[j][1][0]}")
                  # print(f"sum{j} = ",sum)
          mtrk[i][1][0]=sum/mtrk[i][0][i]
          K1.append(mtrk[i][1][0])
      for i in range(len(mtrk)):
          mtrk[i][1][0]=K1[i]
      K1.clear()
      print(f"Perulangan {k+1}")
      for i in mtrk:
          print(i)
  
  
  ```

  Output 

  ```
  Perulangan 1[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.2727272727272727], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [2.388429752066116], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [0.18429752066115707], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.2523760330578513], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [0.34901859504132215], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [0.5], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-3.0], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.5], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [1.5], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 2[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.0292543200601052], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [2.14612774059149], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.116000486647087], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.3245747120671403], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [0.9269577433448872], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [0.75], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-3.1666666666666665], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.75], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 3[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.0173527176238686], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.848545789523982], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.3694918266989948], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.280155799339688], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [2.0026999519942397], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.583333333333333], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.9444444444444446], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 4[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9190824833373884], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.887452623834604], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.197611209905604], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.1282774819356542], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.2972007268622079], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.2638888888888893], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.6296296296296293], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0000000000000009], [-4]]Perulangan 5[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9619811007672648], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.8972157959299571], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.1893839294039292], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.135128401900406], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.422285008291761], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.7384259259259247], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.419753086419752], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.9999999999999996], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0000000000000004], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 6[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9626902409545427], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.9329085565680892], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.0958423770354169], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.0653316397260073], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.1838675401286745], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.7110339506172867], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.2798353909465017], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 7[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9770661429041237], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.9530090899717807], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.0784428387386176], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.0547916416387966], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.1755450424481158], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.8646476337448545], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.186556927297668], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 8[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9827281130541191], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.969706766276004], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.044942403904392], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.030438263676852], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.0913862284860834], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.8811192558299048], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.1243712848651115], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.9999999999999991], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [1.9999999999999991], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 9[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9893008779825128], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.9793307759955923], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.0336456030192895], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.0232148012797595], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.0738517564583185], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.9350690872199339], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.0829141899100754], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 10[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [0.9924456132952312], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.9864791276580334], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.0205956590252885], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.0139929476703058], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [1.0427670482492308], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.9495512664799577], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.0552761266067168], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]
  ```

  

- Metode Gauss Seidell

  digunakan untuk menyelesaikan suatu persamaan linier yang memiliki banyak persamaan. Metode ini menggunakan proses iterasi yang sehingga didapat nilai - nilai yang berubah.

  Jika terdapat persamaan:
  $$
  a_{11}x_{1} + a_{12}x_{2}+...+a_{1n}x_{n} = y_{1}
  $$

  $$
  a_{21}x_{1} + a_{22}x_{2}+...+a_{2n}x_{n} = y_{2}
  $$

  $$
  a_{31}x_{1} + a_{32}x_{2}+...+a_{3n}x_{n} = y_{3}
  $$

  $$
  .
  .
  .
  $$

  $$
  a_{m1}x_{1} + a_{m2}x_{2}+...+a_{mn}x_{n} = y_{m}
  $$

  maka berikan nilai awal untuk setiap Xi (i = 1, 2, 3, ... , m)
  $$
  x_{1} = \dfrac{1}{a_{11}}(y_{1}-a_{12}x_{2}-a_{13}x_{3}-...-a_{1n}x_{n})
  $$

  $$
  x_{2} = \dfrac{1}{a_{21}}(y_{2}-a_{22}x_{2}-a_{23}x_{3}-...-a_{2n}x_{n})
  $$

  $$
  ...
  $$

  $$
  x_{m} = \dfrac{1}{a_{m1}}(y_{m}-a_{m2}x_{2}-a_{m3}x_{3}-...-a_{mn}x_{n})
  $$

  Algoritma untuk metode Gauss-Seidel

  - Menentukan persamaan linear yang akan dikerjakan
  - Membuat bentuk matrik
  - Menentukan nilai awal dari Xi (i=1, 2, ..., n)
  - Substitusikan nilai awal Xi pada rumus seperti di atas.

  Source Code (Python)

  ```
  mtrk=[    [[11,-1,2,0,2,1,1,1,2,3],["X1"],[14]],    [[-1,11,-1,3,1,2,2,2,1,1],["X2"],[25]],    [[2,-1,10,-1,0,1,-2,1,3,3],["X3"],[2]],    [[0,3,-1,8,1,0,2,-1,2,2],["X4"],[17]],    [[1,2,0,1,2,-1,0,1,-3,4],["X5"],[8]],    [[1,2,0,1,2,2,2,2,2,1],["X6"],[9]],    [[1,2,0,1,2,2,3,0,1,-2],["X7"],[0]],    [[1,2,0,1,2,2,3,2,0,-1],["X8"],[1]],    [[1,2,0,1,2,2,3,2,-2,0],["X9"],[-2]],    [[1,2,0,1,2,2,3,2,-2,-2],["X10"],[-4]],]for a in range(len(mtrk[0][0])):    mtrk[a][1][0]=0for k in range(3):    for i in range(len(mtrk)):        # print(k,i)        Xi=mtrk[i][1][0]        # print("Xi = ",Xi)        sum=mtrk[i][2][0]        # print("sum = ",sum)        for j in range(len(mtrk)):            if j == i :                continue            sum=sum-mtrk[i][0][j]*mtrk[j][1][0]                # print(f"mtrk[i][0][j] ={mtrk[i][0][j]} mtrk[i][1][0] = {mtrk[j][1][0]}")                # print(f"sum{j} = ",sum)        mtrk[i][1][0]=sum/mtrk[i][0][i]    print(f"Perulangan {k+1}")    for i in mtrk:        print(i)
  ```

  Output

  ```
  Perulangan 1[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.2727272727272727], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [2.388429752066116], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [0.18429752066115707], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.2523760330578513], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [0.34901859504132215], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [0.5], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-3.0], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.5], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [1.5], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 2[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.0292543200601052], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [2.14612774059149], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.116000486647087], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.3245747120671403], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [0.9269577433448872], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [0.75], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-3.1666666666666665], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [0.75], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]Perulangan 3[[11, -1, 2, 0, 2, 1, 1, 1, 2, 3], [1.0173527176238686], [14]][[-1, 11, -1, 3, 1, 2, 2, 2, 1, 1], [1.848545789523982], [25]][[2, -1, 10, -1, 0, 1, -2, 1, 3, 3], [-1.3694918266989948], [2]][[0, 3, -1, 8, 1, 0, 2, -1, 2, 2], [1.280155799339688], [17]][[1, 2, 0, 1, 2, -1, 0, 1, -3, 4], [2.0026999519942397], [8]][[1, 2, 0, 1, 2, 2, 2, 2, 2, 1], [-0.583333333333333], [9]][[1, 2, 0, 1, 2, 2, 3, 0, 1, -2], [-2.9444444444444446], [0]][[1, 2, 0, 1, 2, 2, 3, 2, 0, -1], [1.0], [1]][[1, 2, 0, 1, 2, 2, 3, 2, -2, 0], [2.0], [-2]][[1, 2, 0, 1, 2, 2, 3, 2, -2, -2], [1.0], [-4]]
  ```

  
