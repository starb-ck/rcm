---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This page is for testing embedded JavaScript

<p id="demo"></p>

<script>
    fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords/recN9KaBLTbxccBnf', {
    headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
    })
    .then(resp => resp.json())
    .then(json => {
        var render = JSON.stringify(json)
        document.getElementById('demo').innerHTML = render.Description;
        });

</script>

