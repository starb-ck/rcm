---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This website is for testing embedded JavaScript

<p id="demo"></p>

<script>
    async function logMovies() {
    const response = await fetch("http://example.com/movies.json");
    const movies = await response.json();
    document.getElementById("demo").innerHTML = await movies;
</script>

