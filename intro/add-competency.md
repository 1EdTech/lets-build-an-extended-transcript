### <a id="add-competency"></a> Adding a competency

Let's add a competency to our transcript:

```
{
  ...
  "transcriptEntities": {
    "id": "urn:uuid:98f56753-973d-4c2d-865a-f567c9896ed7",
    "type": "TranscriptEntitySet",
    "competencies": [
      {
        "id": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C",
        "type": "Competency",
        "name": "Harnessing Planetary Rotational Energy"
      }
    ]
  }
}
```

After saving your changes, go ahead and upload it to the viewer. What do you see?

Interesting, nothing changed. Where's the competency?

In the Extended Transcript Standard, there's a distinction between transcript entities and records. What we just accomplished is describing that there is a competency, "Harnessing Planetary Rotational Energy"; however, we didn't declare anything about whether the learner achieved mastery of this competency.

Let's change that:

```
{
  ...
  "records": [
    {
      "id": "urn:uuid:327de957-910c-4b8d-bdb4-2efc79ebc0e9",
      "type": "Record",
      "date": "2017-11-01T00:00:00.000Z",
      "result": "Mastered",
      "recordOf": {
        "id": "urn:uuid:ec7fdc47-5787-4992-b49c-d47f400dcee2",
        "type": "TranscriptEntityLink",
        "entityType": "Competency",
        "entityId": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C"
      }
    }
  ],
  "transcriptEntities": {
    "id": "urn:uuid:98f56753-973d-4c2d-865a-f567c9896ed7",
    "type": "TranscriptEntitySet",
    "competencies": [
      {
        "id": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C",
        "type": "Competency",
        "name": "Harnessing Planetary Rotational Energy"
      }
    ]
  }
}
```

A few things to note:
* The value of `date` indicates that the record was last updated on Nov 1, 2017.
* The value of `result` is `"Mastered"`; we're declaring that Amy mastered the referenced competency.
* Both the `TranscriptEntityLink`'s `entityId` and the `Competency`'s `id` have the same value, `"urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C"`. This is how a record references a transcript entity.

> Technical aside: `result` has an open vocabulary; there are no restrictions on what values you can set to result, as long as it is a string.

What about the `Record`'s `id`? Just like the `id` belonging to the entire transcript, it's required, though you may never use it.

So here's what we have so far:

```json
{
  "@context": "https://purl.imsglobal.org/ctx/extended-transcript/v1p0",
  "id": "urn:uuid:f95fe190-9f8d-4576-85c3-7bdfb892ce5c",
  "type": "ExtendedTranscript",
  "createdAt": "2017-04-25T00:00:00.00Z",
  "issuer": {
    "id": "urn:uuid:618374e0-e761-4ccb-813a-db66e1d08310",
    "type": "Issuer",
    "name": "Mars University",
    "url": "http://example.org/mars-u",
    "address": "123 E St NW, Washington, DC 20004",
    "phone": "0000000000",
    "issuingPersonFullName": "Inez Wong"
  },
  "person": {
    "id": "urn:uuid:de15d276-a85d-4341-ba3b-d1fb86fed22c",
    "type": "Person",
    "fullName": "Amy Wong",
    "givenName": "Amy",
    "familyName": "Wong",
    "email": "awong@example.org",
    "phone": "0000000000",
    "mobile": "0000000000",
    "url": "http://example.org/awong",
    "studentId": "123456789",
    "birthDate": "1974-08-14",
    "sourcedId": "0123456789"
  },
  "records": [
    {
      "id": "urn:uuid:327de957-910c-4b8d-bdb4-2efc79ebc0e9",
      "type": "Record",
      "date": "2017-11-01T00:00:00.000Z",
      "result": "Mastered",
      "recordOf": {
        "id": "urn:uuid:ec7fdc47-5787-4992-b49c-d47f400dcee2",
        "type": "TranscriptEntityLink",
        "entityType": "Competency",
        "entityId": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C"
      }
    }
  ],
 "transcriptEntities": {
    "id": "urn:uuid:98f56753-973d-4c2d-865a-f567c9896ed7",
    "type": "TranscriptEntitySet",
    "competencies": [
      {
        "id": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C",
        "type": "Competency",
        "name": "Harnessing Planetary Rotational Energy"
      }
    ]
  }
}
```

You should see something this:

<table class="image">
<caption align="bottom">Our transcript should now have one competency record in it.</caption>
<tr><td><img src="../images/6.png" /></td></tr>
</table>

What if Amy is still working on this competency? Try this:

```
{
  ...
  "records": [
    {
     "id": "urn:uuid:327de957-910c-4b8d-bdb4-2efc79ebc0e9",
     "type": "Record",
     "date": "2017-11-01T00:00:00.000Z",
     "result": "In Progress",
     "recordOf": {
        "id": "urn:uuid:ec7fdc47-5787-4992-b49c-d47f400dcee2",
        "type": "TranscriptEntityLink",
        "entityType": "Competency",
        "entityId": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C"
     },
     "status": {
        "id": "urn:uuid:D4ACF5F3-3627-4739-911F-A61D252D1EC0",
        "type": "RecordStatus",
        "completed": false
     }
    }
  ],
  ...
}
```
