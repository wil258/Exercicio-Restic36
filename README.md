from django.views.generic import ListView
from .models import Item

class ItemListView(ListView):
    model = Item
    template_name = 'items/item_list.html'
    context_object_name = 'items'
class ItemListView(ListView):
    model = Item
    template_name = 'items/item_list.html'
    context_object_name = 'items'
    paginate_by = 10  # Exibe 10 itens por página
class ItemListView(ListView):
    model = Item
    template_name = 'items/item_list.html'
    context_object_name = 'items'
    paginate_by = 10

    def get_queryset(self):
        query = self.request.GET.get('q')
        if query:
            return Item.objects.filter(nome__icontains=query)
        return Item.objects.all()
class ItemListView(ListView):
    model = Item
    template_name = 'items/item_list.html'
    context_object_name = 'items'
    paginate_by = 10

    def get_queryset(self):
        query = self.request.GET.get('q')
        order_by = self.request.GET.get('order_by', 'nome')  # Ordena por nome por padrão
        queryset = Item.objects.all()

        if query:
            queryset = queryset.filter(nome__icontains=query)
        
        return queryset.order_by(order_by)

