---
title: /spooki
layout: page
permalink: /spooki/
---

# SPOOKI Database

Welcome to the Simulated Paranormal Observations and Otherworldly Kryptozoological Investigations (SPOOKI) online database. Entities listed below have been declassified for public release.

## ENTITY DIRECTORY:

<p id="list"></p>

# SELECTED CASE FILE:

<p id="name"></p>
<p id="image"></p>
<p id="description"></p>

<script>
    fileid = ""

    function updateDisplayedFile(fileid) {
        fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords/' + fileid, {
            headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
            })
        .then(resp => resp.json())
     .then(json => {
        var image_url = json.fields.Image[0].thumbnails.large.url
        document.getElementById('name').innerHTML = json.fields.Name;
        document.getElementById('image').innerHTML = '<img src="' + image_url + '"alt="alternative-text" width="' + window.screen.height/3 + '"/>'
        document.getElementById("description").innerHTML = json.fields.Description
        });
    }

    fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords?fields%5B%5D=ID&fields%5B%5D=Name&sort%5B0%5D%5Bfield%5D=ID&sort%5B0%5D%5Bdirection%5D=asc', {
    headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
    })
    .then(resp => resp.json())
    .then(json => {
        console.log(json)
        var liststring = ""

        for (let i = 0; i < json.records.length; i++) {
            id_string = json.records[i].id.toString().trim()
            directory_string = id_string + " - " + json.records[i].fields.ID + ": " + json.records[i].fields.Name
            console.log(id_string)
            liststring += ('<a href="javascript:;" onclick="updateDisplayedFile(\'' + id_string + '\')">' + directory_string + '</a>\n')
        }

        document.getElementById('list').innerHTML = liststring
    })

    </script>


