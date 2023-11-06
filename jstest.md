---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This website is for testing embedded JavaScript

<script>
    fetch('https://reqbin.com/echo/get/json')
   .then(response => response.text())
   .then(text => console.log(text));
</script>

