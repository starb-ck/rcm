---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This page is for testing embedded JavaScript

<p id="list"></p>

<p id="name"></p>
<p id="image"></p>
<p id="description"></p>

<script>
     fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords', {
    headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
    })
    .then(resp => resp.json())
    .then(json => {
        console.log(json)
    })
    </script>

<script>
    fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords/recN9KaBLTbxccBnf', {
    headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
    })
    .then(resp => resp.json())
    .then(json => {
        console.log(json)
        var image_url = json.fields.Image[0].url
        document.getElementById('name').innerHTML = json.fields.Name;
        document.getElementById('image').innerHTML = <img src=image_url alt="alternative-text">
        document.getElementById("description").innerHTML = json.fields.Description
        });

</script>

