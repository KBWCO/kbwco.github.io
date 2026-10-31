---
title: Games
note: This is a list of all the games that were played with friends. For sets created, 
  go to the [Sets page](/sets.html)
---
## Chronological List
{% assign games = site.games | sort: "number" %}
{% for game in games -%}
    {%- capture players -%}
        {%- include players-in-game.html game=game -%}
    {%- endcapture -%}
1. [{{game.title}}]({{game.url}}) ({{game.played-date}})
* {{players | split: "," | join: " vs. "}}
{%- if game.pre-drawn-cards and game.blanks -%}
  {%- assign num-cards = game.pre-drawn-cards | plus: game.blanks %}
* {{num-cards}} cards ({{game.pre-drawn-cards}} existing + {{game.blanks}} blanks)
{%- endif -%}
{%- if game.game-ending-card -%}
  {%- assign card = site.cards | where: "title", game.game-ending-card | first %}
* Ended with: [{{card.title}}]({{card.url}})
{%- endif -%}
{%- if game.game-ending-condition %}
* {{game.game-ending-condition}}
{%- endif %}
{% endfor %}
