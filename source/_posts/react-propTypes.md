---
title: react propTypes
date: 2018-10-15 16:26:37
tags:react
---

react配套的类型检测库——prop-types的运用

<!--more-->

> react配套的类型检测库——prop-types的运用

```bash
yourComponent.propTypes = {
    属性1：属性1的变量类型，
    属性2：属性2的变量类型
    //...
}

import PropTypes from 'prop-types';
yourComponent.propTypes = {
  name：PropTypes.string,   //变量name必须是string类型
  id:PropTypes.number.isRequired    //id变量必须传值，不传值报错 
}

```