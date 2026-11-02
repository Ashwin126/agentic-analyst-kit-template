# Data card: Olist Brazilian E-commerce

**Source:** Olist, a Brazilian online marketplace. Public dataset on Kaggle: [kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).
**Period:** September 2016 to October 2018. **Size:** 99,441 orders.

You do not need to download it today. Read this card and design an agent team that could work with it.

## Five sources (plus two helper tables)

| Source | File | Rows | Key columns | Watch out |
| --- | --- | ---: | --- | --- |
| **Orders** | `olist_orders_dataset.csv` | 99,441 | `order_id`, `customer_id`, `order_status`, 5 timestamps (purchase → delivered), estimated delivery date | 2,965 orders have no delivery date (canceled, shipped, not yet delivered) |
| **Payments** | `olist_order_payments_dataset.csv` | 103,886 | `order_id`, `payment_type`, `payment_installments`, `payment_value` | One order can have up to 29 payment rows. Add them up per order |
| **Reviews** | `olist_order_reviews_dataset.csv` | 99,224 | `order_id`, `review_score` (1–5), `review_comment_message` | Comments are in **Portuguese**. Only 41% of reviews have text. 547 orders have 2+ reviews |
| **Customers** | `olist_customers_dataset.csv` | 99,441 | `customer_id`, `customer_unique_id`, city, state | `customer_id` is new for **every order**. The person is `customer_unique_id` (96,096 people). Only 3.1% bought twice |
| **Sellers** | `olist_sellers_dataset.csv` | 3,095 | `seller_id`, city, state | Linked to orders only through order items |
| *Order items (link table)* | `olist_order_items_dataset.csv` | 112,650 | `order_id`, `product_id`, `seller_id`, `price`, `freight_value` | Up to 21 items per order. 1,278 orders have 2+ sellers |
| *Products (helper)* | `olist_products_dataset.csv` | 32,951 | `product_id`, category (Portuguese), photo count, description length | 610 products have no category. A translation table gives English names |

## How the tables join

```
customers --(customer_id)--> orders --(order_id)--> payments
                               |  \---(order_id)--> reviews
                               |
                         (order_id)
                               v
                          order items --(seller_id)--> sellers
                               \------(product_id)--> products
```

## Three facts to start from

- **8.1%** of delivered orders arrived later than the estimated date. Median delivery time: 10 days.
- Late orders average **2.57 stars**. On-time orders average **4.29 stars**.
- **15%** of all reviews are 1 or 2 stars (14,575 of 99,224).

These are associations from historical data, not proof of cause.
