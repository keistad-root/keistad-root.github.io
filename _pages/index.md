---
layout: defaults/page
permalink: index.html
narrow: true
title: Welcome to Keistad's blog
---

## Who am I? 

{% include components/intro.md %}

## Who is Keistad?

Keistad is nickname of me, Choi. Keistad is pronounced with German. I want to study Physics in German. So, I studied German and I want to make German nickname. Keistad isn't real German name, but please pronounce it with German.

## What I studied and working?

- Making Vacuum Chamber
  - 31 Dec 2020~Current
  - My lab want to search new paradigm, trillision, in colling experiment.
  - We need low vacuum(~1mbar) because of lifetime of alpha particle.
  - I test vacuum chamber to make low vacuum in this project.
- Making SQM 2022 Homepage
  - 28 Apr 2021~Current
  - The SQM (Strangeness in Quark Matter) is a international conference. It will hold in busan if the Covid-19 is end.
  - My role is making SQM 2022 homepage, etc...
- ITS3 Upgrade
  - 16 Apr 2021~Current
  - ALICE team in CERN want to upgrade ITS form 2 to 3 during LS2.
  - I find my role in ITS upgrade project.

  ## Education and experience

- graduated Duksang elementary school (Mar 2005 ~ Feb 2011)
- graduated Silla middle school (Mar 2011 ~ Feb 2014)
- graduated Sungdo high school (Mar 2014 ~ Feb 2017)
- Physics, Pusan national university (Mar 2017 ~ Feb 2019 and Jan 2021 ~ Current)
- Airman in POL, 11th wings (Mar 2019 ~ Jan 2021)
- Intern, HIPEx (Jan 2021 ~ Current)

## How languages can I do?

- Korean : C2
- English : A1
- German : A1

## How programming languages can I do?

- C++(Root) : basic
- Mathematica : basic

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


