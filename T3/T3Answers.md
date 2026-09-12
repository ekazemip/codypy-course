# Django T3 Answers

## 1. Create objects

### Category

```python
>>> from core.models import Item ,Claim ,Category
>>> Category.objects.create(title='Jewelry')
<Category: Jewelry>
>>> Category.objects.create(title='Documents')
<Category: Documents>
```

### User

```python
>>> from django.contrib.auth.models import User
>>> a1 = User.objects.create(username='ali',first_name='ali',last_name='alavi')
>>> a2 = User.objects.create(username='javad',first_name='javad',last_name='javadi')
>>> a3 = User.objects.create(username='fatemeh',first_name='fatemeh',last_name='fatemi')
>>> a1.set_password('ali123')
>>> a2.set_password('javad123')
>>> a2.set_password('fatemeh123')
```

### Item

```python
>>> user_ali = User.objects.get(username='ali')
>>> Item.objects.create(title='cart meli',description='cart meli be nam javad javadi', category=doc_in_cat,status='open ', event_date = "2026-09-26",created_by=user_ali)
<Item: cart meli | open >
>>> user_fatemeh = User.objects.get(username="fatemeh")
>>> doc_in_cat = Category.objects.get(id=4)
>>> doc_in_cat
<Category: Jewelry>
>>> Item.objects.create(title='gardanband', category=doc_in_cat,status='open ', event_date = "2026-09-13",created_by=user_fatemeh)
<Item: gardanband | open >
>>> Item.objects.create(title='daftar 100 barg', category=Category.objects.get(title="Documents"),status='open ', event_date = "2026-09-11",created_by=user_fatemeh)
<Item: daftar 100 barg | open >
>>> Item.objects.create(title='angoshtar', category=doc_in_cat,status='open', event_date = "2026-09-21",created_by=user_ali)
<Item: angoshtar | open>
```

### Claim

```python
>>> item_cart_meli = Item.objects.filter(title='cart meli').first()
>>> user = User.objects.get(username='javad')
>>> Claim.objects.create(item=item_cart_meli,claimant=user,status='pending')
<Claim: Claim object (2)>
>>> user= User.objects.get(username='fatemeh')
>>> Claim.objects.create(item=item_angoshtar,claimant=user,status='pending')
<Claim: Claim object (3)>
```

## 2. Queries

### Q1

```python
>>> q1 = Item.objects.filter(category__title="Jewelry")
>>> q1
<QuerySet [<Item: gardanband | open >, <Item: angoshtar | open>]>
```

### Q2

```python
>>> q2 = Item.objects.filter(created_by__username="ali")
>>> q2
<QuerySet [<Item: cart meli | open >, <Item: angoshtar | open>]>
```

### Q3

```python
>>> q3 = Claim.objects.filter(item__title="cart meli")
>>> q3
<QuerySet [<Claim: Claim object (2)>]>
```

### Q4

```python
>>> q4 = Claim.objects.filter(claimant__username="fatemeh")
>>> q4
<QuerySet [<Claim: Claim object (3)>]>
>>> claim1 = q4.first()
<Item: angoshtar | open>
```
