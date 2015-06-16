---
layout: default
---
{% if site.conference.twitterhash %}
<a class="twitter-timeline" href="https://twitter.com/hashtag/{{ site.conference.twitterhash }}" data-widget-id="610697182967107584">#{{ site.conference.twitterhash }} Tweets</a>
<script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+"://platform.twitter.com/widgets.js";fjs.parentNode.insertBefore(js,fjs);}}(document,"script","twitter-wjs");</script>
{% endif %}

**{{ site.conference.location }}**,
{% assign startdate = site.conference.dates | first %}
{% assign enddate = site.conference.dates | last %}
{% if startdate.month == enddate.month %}
{{ startdate.date }} - {{ enddate.date }} {{ startdate.month }} {{ startdate.year }}<br>
{% else %}
{{ startdate.date }} {{ startdate.month }} - {{ enddate.date }} {{ enddate.month }} {{ startdate.year }}
{% endif %}
{% if site.conference.hosturl %} [Hosts Local Page]({{ site.conference.hosturl }})<br>{% endif %}
{% if site.conference.organizers %} organized by {% for person in site.conference.organizers %}[{{ person.name }}]({{ person.url }}){% if site.conference.organizers | size > 1 %}, {% endif %}{% endfor %}{% endif %}

{% if site.conference.hosts %}hosted by {% for person in site.conference.hosts %}[{{ person.name }}]({{ person.url }}){% if site.conference.hosts | size > 1 %}, {% endif %}{% endfor %}{% endif %}

# {% if site.conference.draft == "Y" %} Draft Schedule {% else %} Schedule {% endif %}
{% for date in site.conference.dates %}
## {{ date.day }} {{ date.date }} {{ date.month }} 
{% for slot in site.data.lectures %}
{% assign thedate = slot.date | plus: 0%}
{% if date.date == thedate %}
{% if slot.start %}{{ slot.start }} {% if slot.end %}- {{ slot.end }} {% endif %}{% endif %}{% if slot.pdf %}[{{ slot.title }}]({{ slot.pdf }}){% else %}{{ slot.title }}{% endif %}{% if slot.speaker %}, {{ slot.speaker }}{% endif %}{% if slot.institution %}, {{ slot.institution }}{% endif %}{% if slot.ipynb %} [[code]({{ slot.ipynb }})]{% endif %}
{% if slot.youtube %}
<iframe width="{{ site.youtube.width }}" height="{{ site.youtube.height }}" src="https://www.youtube.com/embed/{{ slot.youtube }}" frameborder="0" allowfullscreen></iframe>
{% endif %}
{% endif %}
{% endfor %}
{% endfor %}

