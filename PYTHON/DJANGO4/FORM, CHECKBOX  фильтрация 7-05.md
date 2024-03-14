1.
goods.templates.goods.catalog.html
```html
<!-- ---------------------------------------------------------------------------------------------- -->  
<!-- ---------------------------------------------------------------------------------------------- -->  
<!-- ---------------------------------------------------------------------------------------------- -->  
    <!-- Форма фильтров -->    <div class="dropdown mb-2">  
        <button class="btn btn-secondary dropdown-toggle btn-dark" type="button" data-bs-toggle="dropdown"  
            aria-expanded="false">  
            Фильтры  
        </button>  
  
        <form action="{% url 'catalog:index' slug_url %}" method="get" class="dropdown-menu bg-dark" data-bs-theme="dark">  
            <!-- action - url куда будет отправлен запрос -->  
            <div class="form-check text-white mx-3">  
                <input class="form-check-input" type="checkbox" name="on_sale" id="flexCheckDefault" value="on">  
                <!-- передаст параметр on_sale=on -->  
                <input type="hidden" name="q" value="request.GET.q">  
                <label class="form-check-label" for="flexCheckDefault">  
                    Товары по акции  
                </label>  
            </div>            <p class="text-white mx-3 mt-3">Сортировать:</p>  
            <div class="form-check text-white mx-3">  
                <input class="form-check-input" type="radio" name="order_by" id="flexRadioDefault1" value="default" checked>  
                <label class="form-check-label" for="flexRadioDefault1">  
                    По умолчанию  
                </label>  
            </div>            <div class="form-check text-white mx-3">  
                <input class="form-check-input" type="radio" name="order_by" id="flexRadioDefault2" value="price">  
                <label class="form-check-label" for="flexRadioDefault2">  
                    От дешевых к дорогим  
                </label>  
            </div>            <div class="form-check text-white mx-3">  
                <input class="form-check-input" type="radio" name="order_by" id="flexRadioDefault3" value="-price">  
                <label class="form-check-label" for="flexRadioDefault3">  
                    От дорогих к дешевым  
                </label>  
            </div>            <button type="submit" class="btn btn-primary mx-3 mt-3">Применить</button>  
        </form>    </div><!-- ---------------------------------------------------------------------------------------------- -->  
<!-- ---------------------------------------------------------------------------------------------- -->  
<!-- ---------------------------------------------------------------------------------------------- -->
```


goods.viwes.py
```python
def catalog(request, category_slug):  
  
    page = request.GET.get('page', 1)  
  
    if category_slug == 'all':  
        goods = Products.objects.all()  
    else:  
        goods = get_list_or_404(Products.objects.filter(category__slug=category_slug))  
  
    paginator = Paginator(goods, 3) # goods в любом случае проходит через пагинатор  
    current_page = paginator.page(int(page))  
  
    context = {  
        "title": "Home - Каталог",  
        "goods": current_page,  
        "slag_url": category_slug  
    }  
    return render(request, 'goods/catalog.html', context)
```

