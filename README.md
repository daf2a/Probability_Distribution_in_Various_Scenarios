# Laporan Praktikum Probabilitas dan Statistika

## Pendahuluan

Laporan praktikum ini disusun sebagai tugas dari mata kuliah Probabilitas dan Statistika kelas C. Praktikum ini membahas tentang distribusi probabilitas dan penggunaan distribusi tersebut dalam beberapa contoh kasus.

Nama Praktikan  : Muhammad Daffa Ashdaqfillah\
NRP Praktikan   : 5025211015

## Modul I Distribusi Probabilitas

### 1. Pendistribusian Banyak Bayi Laki-laki

a. Pendistribusian banyak bayi laki-laki mengikuti distribusi binomial dengan parameter n = 10 dan p = 0,488.

```
library(ggplot2)
library(dplyr)

p_laki_laki <- 0.488
n_bayi <- 10

pendistribusian_bayi_laki_laki <- data.frame(x = 0:n_bayi) %>%
    mutate(prob = dbinom(x, n_bayi, p_laki_laki))

ggplot(pendistribusian_bayi_laki_laki, aes(x, prob)) +
    geom_bar(stat = "identity") +
    ggtitle("Pendistribusian Banyak Bayi Laki-laki") +
    xlab("Banyak Bayi Laki-laki") +
    ylab("Probabilitas")

```

b. Probabilitas tepat 3 bayi berjenis kelamin laki-laki adalah:

```
p_tepat_3_laki_laki <- dbinom(3, n_bayi, p_laki_laki)
p_tepat_3_laki_laki

```

c. Probabilitas kurang dari 3 bayi berjenis kelamin laki-laki adalah:

```
p_kurang_dari_3_laki_laki <- pbinom(2, n_bayi, p_laki_laki)
p_kurang_dari_3_laki_laki

```

d. Probabilitas tiga atau lebih bayi berjenis kelamin laki-laki adalah:

```
p_tiga_atau_lebih_laki_laki <- sum(dbinom(3:n_bayi, n_bayi, p_laki_laki))
p_tiga_atau_lebih_laki_laki

```

e. Nilai harapan banyak bayi laki-laki adalah:

```
mu_banyak_bayi_laki_laki <- n_bayi * p_laki_laki
mu_banyak_bayi_laki_laki

```

Nilai simpangan baku banyak bayi laki-laki adalah:

```
sigma_banyak_bayi_laki_laki <- sqrt(n_bayi * p_laki_laki * (1 - p_laki_laki))
sigma_banyak_bayi_laki_laki

```

f. Histogram pendistribusian banyak bayi laki-laki:

```
ggplot(pendistribusian_bayi_laki_laki, aes(x)) +
    geom_histogram(aes(y = ..density..), binwidth = 1, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    ggtitle("Histogram Pendistribusian Banyak Bayi Laki-laki") +
    xlab("Banyak Bayi Laki-laki") +
    ylab("Density")

```

### 2. Pendistribusian Banyak Kematian akibat Kanker Tulang

a. Pendistribusian banyak kematian akibat kanker tulang mengikuti distribusi Poisson dengan parameter λ = 1,8.

```
lambda_kematian_tulang <- 1.8

pendistribusian_kematian_tulang <- data.frame(x = 0:10) %>%
    mutate(prob = dpois(x, lambda_kematian_tulang))

ggplot(pendistribusian_kematian_tulang, aes(x, prob)) +
    geom_bar(stat = "identity") +
    ggtitle("Pendistribusian Banyak Kematian Akibat Kanker Tulang") +
    xlab("Banyak Kematian") +
    ylab("Probabilitas")

```

b. Probabilitas 4 kematian akibat kanker tulang di antara pekerja pabrik ban adalah:

```
p_4_kematian_tulang <- dpois(4, lambda_kematian_tulang)
p_4_kematian_tulang

```

c. Peluang paling banyak 4 kematian akibat kanker tulang adalah:

```
p_paling_banyak_4_kematian_tulang <- ppois(4, lambda_kematian_tulang)
p_paling_banyak_4_kematian_tulang

```

d. Peluang lebih dari 4 kematian akibat kanker tulang adalah:

```
p_lebih_dari_4_kematian_tulang <- 1 - p_paling_banyak_4_kematian_tulang
p_lebih_dari_4_kematian_tulang

```

e. Nilai harapan banyak kematian akibat kanker tulang adalah:

```
mu_banyak_kematian_tulang <- lambda_kematian_tulang
mu_banyak_kematian_tulang

```

Nilai simpangan baku banyak kematian akibat kanker tulang adalah:

```
sigma_banyak_kematian_tulang <- sqrt(lambda_kematian_tulang)
sigma_banyak_kematian_tulang

```

f. Histogram pendistribusian banyak kematian akibat kanker tulang:

```
ggplot(pendistribusian_kematian_tulang, aes(x)) +
    geom_histogram(aes(y = ..density..), binwidth = 1, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    ggtitle("Histogram Pendistribusian Banyak Kematian Akibat Kanker Tulang") +
    xlab("Banyak Kematian") +
    ylab("Density")

```

g. Simulasi pendistribusian banyak kematian akibat kanker tulang:

```
banyak_simulasi <- 10000

simulasi_kematian_tulang <- rpois(banyak_simulasi, lambda_kematian_tulang)

ggplot(data.frame(kematian_tulang = simulasi_kematian_tulang), aes(kematian_tulang)) +
    geom_histogram(aes(y = ..density..), binwidth = 1, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    ggtitle("Simulasi Pendistribusian Banyak Kematian Akibat Kanker Tulang") +
    xlab("Banyak Kematian") +
    ylab("Density")

```

h. Berdasarkan hasil simulasi, pendistribusian banyak kematian akibat kanker tulang cenderung simetris dengan nilai rata-rata sekitar 1,8. Hasil simulasi sejalan dengan jawaban pada pertanyaan 2d.

### 3. Distribusi Chi-Square

a. Fungsi probabilitas dari distribusi Chi-Square dengan v = 10 adalah:

```
v_chi_square <- 10

x_chi_square <- seq(0, 30, 0.1)
y_chi_square <- dchisq(x_chi_square, v_chi_square)

ggplot(data.frame(x = x_chi_square, y = y_chi_square), aes(x, y)) +
    geom_line() +
    ggtitle("Fungsi Probabilitas Distribusi Chi-Square") +
    xlab("x") +
    ylab("f(x)")

```

b. Histogram dari distribusi Chi-Square dengan 500 data acak:

```
banyak_data_chi_square <- 500

simulasi_chi_square <- rchisq(banyak_data_chi_square, v_chi_square)

ggplot(data.frame(chi_square = simulasi_chi_square), aes(chi_square)) +
    geom_histogram(aes(y = ..density..), binwidth = 1, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    ggtitle("Histogram Distribusi Chi-Square") +
    xlab("x") +
    ylab("Density")

```

c. Nilai rataan (μ) dan varian (σ²) dari distribusi Chi-Square dengan v = 10 adalah:

```
mu_chi_square <- v_chi_square
mu_chi_square

sigma_chi_square <- sqrt(2 * v_chi_square)
sigma_chi_square

```

### 4. Distribusi Normal

a. Fungsi probabilitas dari distribusi Normal dengan mean = 45 dan sd = 5 adalah:

```
mean_normal <- 45
sd_normal <- 5

x_normal <- seq(0, 90, 0.1)
y_normal <- dnorm(x_normal, mean_normal, sd_normal)

ggplot(data.frame(x = x_normal, y = y_normal), aes(x, y)) +
    geom_line() +
    ggtitle("Fungsi Probabilitas Distribusi Normal") +
    xlab("x") +
    ylab("f(x)")

```

Probabilitas P(X1 ≤ x ≤ X2), dengan X1 = 5 dan X2 = 6 adalah:

```
x1 <- 5
x2 <- 6

p_normal <- pnorm(x2, mean_normal, sd_normal) - pnorm(x1, mean_normal, sd_normal)
p_normal

```

z-score untuk X1 adalah:

```
z_x1 <- (x1 - mean_normal) / sd_normal
z_x1

```

z-score untuk X2 adalah:

```
z_x2 <- (x2 - mean_normal) / sd_normal
z_x2

```

Plot data bangkitan acak dalam bentuk grafik:

```
data_normal <- c(11, 1, 2, 4, 2, 6, 3, 10, 11, 5, 3, 6, 8)

x1 <- floor(mean(data_normal))
x2 <- ceiling(mean(data_normal))

ggplot(data.frame(data = data_normal), aes(data)) +
    geom_histogram(aes(y = ..density..), binwidth = 1, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    geom_vline(xintercept = x1, color = "red", size = 1) +
    geom_vline(xintercept = x2, color = "red", size = 1) +
    ggtitle("Histogram Distribusi Normal") +
    xlab("x") +
    ylab("Density")

```

b. Histogram dari distribusi Normal dengan breaks = 50:

```
ggplot(data.frame(x = x_normal, y = y_normal), aes(x)) +
    geom_histogram(aes(y = ..density..), breaks = 50, color = "black", fill = "white") +
    geom_density(alpha = .2, fill = "#FF6666") +
    ggtitle("Histogram Distribusi Normal") +
    xlab("x") +
    ylab("Density")

```

c. Nilai varian (σ²) dari hasil data bangkitan acak distribusi Normal adalah:

```
var_normal <- var(data_normal)
var_normal

```

### 5. Distribusi T-Student

a. Probabilitas terjadinya suatu peristiwa acak X kurang dari -2,34 dengan 6 derajat kebebasan adalah:

```
df_t <- 6
x_t1 <- -2.34

p_t1 <- pt(x_t1, df_t)
p_t1

```

b. Probabilitas terjadinya suatu peristiwa acak X lebih dari 1,34 dengan 6 derajat kebebasan adalah:

```
x_t2 <- 1.34

p_t2 <- 1 - pt(x_t2, df_t)
p_t2

```

c. Probabilitas terjadinya suatu peristiwa acak X kurang dari -1,23 atau lebih besar dari 1,23 dengan 3 derajat kebebasan adalah:

```
df_t2 <- 3
x_t3 <- -1.23
x_t4 <- 1.23

p_t3 <- pt(x_t3, df_t2) + (1 - pt(x_t4, df_t2))
p_t3

```

d. Probabilitas terjadinya suatu peristiwa acak X berada di antara -0,94 dan 0,94 dengan 14 derajat kebebasan adalah:

```
df_t3 <- 14
x_t5 <- -0.94
x_t6 <- 0.94

p_t4 <- pt(x_t6, df_t3) - pt(x_t5, df_t3)
p_t4

```

e. Nilai t-score dengan 5 derajat kebebasan yang memiliki luasan 0,0333 satuan persegi di bawah kurva dan di sebelah kiri t-score tersebut adalah:

```
df_t4 <- 5
p_t5 <- 0.0333

x_t7 <- qt(p_t5, df_t4, lower.tail = TRUE
```