---
title: Games
note: This is a list of all the games that were played with friends. For sets created, 
  go to the [Sets page](/sets.html)
---
## Chronological List
{%- assign games = site.games | sort: "number" -%}
{%- assign num-created-cards-overall = 0 %}
{% for game in games -%}
    {%- capture players -%}
        {%- include players-in-game.html game=game -%}
    {%- endcapture -%}
    {%- capture all-cards-created -%}
        {%- include cards-created-in-game.html game=game -%}
    {%- endcapture -%}
    {%- assign num-cards-created = all-cards-created | split: ":==!:" | size -%}
    {%- assign num-created-cards-overall = num-created-cards-overall | plus: num-cards-created -%}
1. [{{game.title}}]({{game.url}}) ({{game.played-date}})
* {{players | split: "," | join: " vs. "}}
{%- if game.pre-drawn-cards and game.blanks -%}
  {%- assign num-cards = game.pre-drawn-cards | plus: game.blanks %}
* {{num-cards}} cards ({{game.pre-drawn-cards}} existing + {{game.blanks}} blanks)
{%- endif %}
* {{num-cards-created}} cards created during game, {{num-created-cards-overall}} overall
{%- if game.game-ending-card -%}
  {%- assign card = site.cards | where: "title", game.game-ending-card | first %}
* Ending Card: [{{card.title}}]({{card.url}})
{%- endif -%}
{%- if game.game-ending-condition %}
* Ending Condition: {{game.game-ending-condition}}
{%- endif %}
{% endfor %}
