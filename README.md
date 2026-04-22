# festival

Descreva aqui as alterações/correções que fez
- no urls.py faltava: 

path('dias/', views.dias_view, name='dias'),

no views.py:

- adição de:

def palcos_view(request):
    palcos = Palco.objects.all().order_by('nome')

    context = {'palcos': palcos}

    return render(request, 'festival/palcos.html', context)


- Import em falta:

from .models import Dia, Palco, Concerto


- concerto_view incompleto, correção: 

def concerto_view(request, id):
    concerto = Concerto.objects.get(id=id)

    context = {'concerto': concerto}

    return render(request, 'festival/concerto.html')

- Nos templates, falta o dias.html:

{% extends 'festival/layout.html' %}

{% block title %}Dias{% endblock %}

{% block content %}
<h2>Lista de Dias</h2>

{% if dias %}
    <ul>
        {% for dia in dias %}
            <li>{{ dia.data }}</li>
        {% endfor %}
    </ul>
{% else %}
    <p>Não existem dias registados.</p>
{% endif %}

{% endblock %}

