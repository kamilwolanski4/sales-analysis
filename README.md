# sales-analysis 🛒📊

Projekt typu **end-to-end EDA (Exploratory Data Analysis)** wykonany na danych e-commerce (Olist) w celu zrozumienia struktury zamówień, identyfikacji braków danych, analizy rozkładów cen i kosztów dostawy oraz sprawdzenia zależności pomiędzy cechami produktów a logistyką.

## 🎯 Cel projektu (EDA)

Celem analizy było:

- zrozumienie struktury danych (**orders + order_items + products**)
- analiza brakujących wartości oraz potencjalnych przyczyn ich występowania
- analiza rozkładu cen produktów, kosztów dostawy oraz kategorii
- sprawdzenie zależności:
  - cena / koszt dostawy (freight)
  - cechy produktu (waga, wymiary) / koszt dostawy
- identyfikacja wartości odstających (outliers)

---

## 📦 Dane

Projekt wykorzystuje dane Olist (brazylijski e-commerce):

- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_products_dataset.csv`

Po połączeniu tabel otrzymano finalny dataframe:

- **113 425 rekordów**
- **22 kolumny**

---

## 🧩 Kolumny wykorzystane w analizie

- `order_id` – identyfikator zamówienia  
- `customer_id` – identyfikator klienta  
- `order_status` – status zamówienia  
- `order_purchase_timestamp` – moment zakupu  
- `order_approved_at` – moment zatwierdzenia zamówienia  
- `order_delivered_carrier_date` – przekazanie paczki kurierowi  
- `order_delivered_customer_date` – dostarczenie paczki do klienta  
- `order_estimated_delivery_date` – szacowana data dostawy  
- `order_item_id` – numer pozycji w zamówieniu  
- `product_id` – identyfikator produktu  
- `seller_id` – identyfikator sprzedawcy  
- `shipping_limit_date` – deadline dla sprzedawcy  
- `price` – cena produktu  
- `freight_value` – koszt transportu  
- `product_category_name` – kategoria produktu  
- `product_name_lenght` – długość nazwy produktu  
- `product_description_lenght` – długość opisu produktu  
- `product_photos_qty` – liczba zdjęć produktu  
- `product_weight_g` – waga produktu (g)  
- `product_length_cm` – długość produktu (cm)  
- `product_height_cm` – wysokość produktu (cm)  
- `product_width_cm` – szerokość produktu (cm)

---

## ❗ Brakujące dane

Zidentyfikowane braki danych wraz z udziałem procentowym:

- 161 braków w `order_approved_at` (**0.14%**)
- 1 968 braków w `order_delivered_carrier_date` (**1.74%**)
- 3 229 braków w `order_delivered_customer_date` (**2.85%**)
- 775 braków danych produktowych (**0.68%**)
- 2 378 braków w `product_category_name` i kolumnach powiązanych (**2.10%**)
- 793 braki w parametrach gabarytowych produktu (**0.70%**)

📌 Wnioski:  
Braki w danych produktowych najczęściej dotyczyły zamówień o statusie **unavailable**, co jest dość logiczne ponieważ produkt nie był dostępny więc brak pełnych informacji.

---

## 💰 Analiza cen produktów

Podstawowe statystyki cen:

- Min: **0.85**
- Max: **6 725**
- Średnia: **120.65**
- Mediana: **75**
- Odchylenie standardowe: **183.63**

📌 Wniosek:  
Średnia jest większa od mediany → rozkład jest prawostronnie skośny, a w danych występują drogie outliery.

---

## 📊 Liczba sprzedanych sztuk w przedziałach cenowych

Przedziały cenowe (price_group) i liczba sprzedanych produktów:

- 0–2: **23**
- 3–10: **1 246**
- 11–20: **8 132**
- 21–50: **29 916**
- 51–100: **33 020**
- 101–500: **37 097**
- 501–1500: **2 882**
- 1501+: **334**

📌 Wniosek:  
Zdecydowana większość sprzedaży odbywa się w przedziale **21–500**.

---

## 🚚 Koszt dostawy (freight_value)

Statystyki kosztu dostawy:

- Min: **0**
- Max: **409.68**
- Średnia: **19.99**
- Mediana: **16.26**
- Odchylenie standardowe: **15.8**

---

## 🏷️ Najpopularniejsze kategorie (Top10)

Najczęściej kupowane kategorie produktów (liczone jako liczba pozycji zamówień):

- cama_mesa_banho – **11 115**
- beleza_saude – **9 670**
- esporte_lazer – **8 641**
- moveis_decoracao – **8 334**
- informatica_acessorios – **7 827**
- utilidades_domesticas – **6 964**
- relogios_presentes – **5 991**
- telefonia – **4 545**
- ferramentas_jardim – **4 347**
- automotivo – **4 235**

---

## ⏱️ Czas dostawy

Dla zamówień ze statusem **delivered** policzono czas dostawy:

- Min: **0 dni**
- Max: **209 dni** *(outlier)*
- Średnia: **12 dni**
- Mediana: **10 dni**

---

## 🔗 Relacje między zmiennymi (korelacje)

Wybrane zależności z macierzy korelacji:

### Korelacja nr 1
✅ Cena i koszt dostawy mają umiarkowaną dodatnią korelację:  
**r = 0.41**

### Korelacja nr 2
✅ Cena i waga produktu mają umiarkowaną dodatnią korelację:  
**r = 0.34**

### Korelacja nr 3
✅ Najsilniej z kosztem dostawy koreluje waga produktu:  
**r = 0.61**

📌 Wniosek:  
Koszt dostawy jest bardziej zależny od cech produktu (gabaryty/waga) niż od samej ceny.

---

## 🚨 Wartości odstające (outliers)

W analizie wykorzystano metodę IQR (Q1/Q3 i 1.5×IQR).

### Najwyższe ceny produktów (Top3)
- 6 735
- 6 729
- 6 499

### Najwyższe koszty dostawy (Top3)
- 409.68
- 375.28
- 375.28

### Największe wagi produktu (Top3)
- 40 425 g
- 40 425 g
- 30 000 g

---

## 🧠 Technologie

- Python
- Pandas
- Matplotlib
- Jupyter Notebook

---

## 📁 Struktura repozytorium
sales-analysis/
│
├── README.md
├── .gitignore
└── notebooks/
└── 01_eda_sales.ipynb
