---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This website is for testing embedded JavaScript

<p id="demo"></p>

<script>
    fetch('https://ubahthebuilder.tech/posts/1')
    .then(data => {
    return data.json();
    })
    .then(post => {
    console.log(post.title);
    });
</script>

