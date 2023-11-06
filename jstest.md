---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This website is for testing embedded JavaScript

<p id="demo"></p>

<script>
    fetch('https://reqbin.com/echo/get/json', {
    headers: {Authorization: 'Bearer {token}'}
    })
    .then(resp => resp.json())
    .then(json => console.log(JSON.stringify(json)))
</script>

