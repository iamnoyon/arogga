# Arogga Web Crawler

This project showcases a custom web crawler developed to extract comprehensive product information from arogga.com including categories, product names, URLs, SKUs, images, prices, and discount prices and many more

---

## Key Features

- Collects data from all products and categories on Arogga.
- Extracts essential product information:
  - **Product Name, Product URL, SKU, Image URL, Brand, Product Type, Generic Name, Original URL, Format**
  - **Price, Discount Price, Crossed Out Price, Unit Price, Unit Crossed Out Price, Availability, Ordered Count, Wishlist Count, Viewed Count, Rating, Discount Claim**
  - **AND MANY MORE**
- Supports **multithreading** for efficient scraping.
- Database storage via **PostgreSQL**.
- Implements **Regex**, **JSON** parsing, and **data cleaning**.

---

## Sample Product Query & Result
```sql
select p.id, p.name, p.brand, p.product_type, p.generic_name, p.url, p.original_url, p.image_url, p.sku, p.format_full, h.price, h.crossed_out_price, h.discount_claim, h.unit_price, h.unit_crossed_out_price, h.availability,h.ordered_count, h.wishlist_count, h.viewed_count, h.rating from product p join history h on p.id=h.product_id order by random() limit 5;

  id   |                       name                        |                 brand                 | product_type |             generic_name              |                                         url                                          |                                     original_url                                      |                                 image_url                                  |   sku   |      format_full       | price  | crossed_out_price | discount_claim | unit_price | unit_crossed_out_price | availability | ordered_count | wishlist_count | viewed_count | rating
-------+---------------------------------------------------+---------------------------------------+--------------+---------------------------------------+--------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+----------------------------------------------------------------------------+---------+------------------------+--------+-------------------+----------------+------------+------------------------+--------------+---------------+----------------+--------------+--------
  2216 | Cathy Doll Acne Oil Control Cleansing Foam 150ml  | Cathy Doll                            | beauty       |                                       | https://www.arogga.com/product/53760?pv_id=53760                                     | https://www.arogga.com/product/53760/cathy-doll-acne-oil-control-cleansing-foam-150ml | https://www.arogga.com/_next/static/media/v1_default_beauty.cfd68d5f.png   | 53760   | 150ml tube             |  466.4 |               530 | 13% OFF        |      466.4 |                    530 | Out of stock |             1 |              2 |          228 |    4.9
 30944 | KT Gold Plus Cream Pearl Cream 10gm               | KT Brand                              | beauty       |                                       | https://www.arogga.com/product/66654/kt-gold-plus-cream-pearl-cream-10gm?pv_id=66756 | https://www.arogga.com/product/66654/kt-gold-plus-cream-pearl-cream-10gm              | https://www.arogga.com/_next/static/media/v1_default_beauty.cfd68d5f.png   | ARG-MED | 10gm Jar               |    396 |               450 | 12% OFF        |        396 |                    450 | In stock     |             1 |              1 |           40 |    4.9
 15398 | Saliben 6%+3% Ointment                            | Amico Laboratories Ltd.               | medicine     | Benzoic Acid 6% + Salicylic Acid 3%   | https://www.arogga.com/product/23234?pv_id=23234                                     | https://www.arogga.com/product/23234/saliben-ointment-63                              | https://www.arogga.com/_next/static/media/v1_default_medicine.345a1601.png | 23234   | 6%+3% (Ointment)       |   22.5 |                25 | 10% OFF        |       22.5 |                     25 | In stock     |            10 |              1 |         1097 |    4.9
 38354 | TPC 30's Container Tablet                         | The ACME Laboratories Ltd.            | medicine     | Vitamin B1 + Vitamin B6 + Vitamin B12 | https://www.arogga.com/product/23256?pv_id=23256                                     | https://www.arogga.com/product/23256/tpc-30s-container-tablet                         | https://www.arogga.com/_next/static/media/v1_default_medicine.345a1601.png | 23256   | Tablet                 | 297.42 |               330 | 10% OFF        |      9.914 |                     11 | Out of stock |           258 |              3 |        30222 |    4.9
  6599 | Sinatide 250 Cozycap 50mcg+250mcg Capsule         | The Ibn Sina Pharmaceutical Ind. Ltd. | medicine     | Salmeterol + Fluticasone              | https://www.arogga.com/product/59140?pv_id=59140                                     | https://www.arogga.com/product/59140/sinatide-250-cozycap-capsule-50mcg250mcg         | https://www.arogga.com/_next/static/media/v1_default_medicine.345a1601.png | 59140   | 50mcg+250mcg (Capsule) |     81 |                90 | 11% OFF        |        8.1 |                      9 | In stock     |            11 |              2 |         1655 |    4.9
(5 rows)
