---
title: /jstest
layout: page
permalink: /jstest/
---

# js-test

This website is for testing embedded JavaScript

<p id="demo"></p>

<script>
    var Airtable = require('airtable');
    var base = new Airtable({apiKey: 'patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}).base('appoMmtp6PrLl2ykz');

    base('EntityRecords').find('recN9KaBLTbxccBnf', function(err, record) {
        if (err) { console.error(err); return; }
        console.log('Retrieved', record.id);
    });
</script>

