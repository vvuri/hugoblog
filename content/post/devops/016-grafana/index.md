---
categories: ["Code"]
tags: ["Grafana"]
description: ""
menu: 
    main:
        parent: "DevOps"
date: "2019-01-20"
title: "Начало работы с Grafana"
---

Grafana -  это платформа для визуализации, мониторинга и анализа данных.
- [основной сайт](https://grafana.com/)
- [Download](https://grafana.com/grafana/download)
<!--more-->
- Debian install
  ```
  $ wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_4.6.2_amd64.deb
  $ sudo dpkg -i grafana_4.6.2_amd64.deb
  ```
 - Standalone Windows 
  ```
  $ wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.6.2.windows-x64.zip
  $ unzip grafana-4.6.2.windows-x64.zip
  ```
- есть куча готовых [дашбордов](https://grafana.com/dashboards)