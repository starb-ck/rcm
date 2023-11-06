---
title: /jstest
layout: page
permalink: /jstest/
---

# ENTITY DIRECTORY:

<p id="list"></p>

# BEGIN FILE:

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

    fetch('https://api.airtable.com/v0/appoMmtp6PrLl2ykz/EntityRecords', {
    headers: {Authorization: 'Bearer patCJRVWZh4svbaze.2dafd7f4bc8a2341936747c7dafb1e36ec3a2149397dd9f3aeabfcf5a6726d0e'}
    })
    .then(resp => resp.json())
    .then(json => {
        console.log(json)
        var liststring = ""

        for (let i = 0; i < json.records.length; i++) {
            id_string = json.records[i].id.toString()
            console.log(id_string)
            liststring += ('<p onclick="updateDisplayedFile("'+id_string+'")">' + id_string + '</p>')
        }

        document.getElementById('list').innerHTML = liststring
    })

    updateDisplayedFile("recN9KaBLTbxccBnf")

    </script>


