# Getting started with the IMS Extended Transcript standard
## Part 1: Let's build an extended transcript!

**TODO: add TOC**

## <a name=""></a> Overview

If you attended a postsecondary institution, you probably know what a transcript is: a document (often physical) with a list of courses and their associated credits and grades issued by the registrar at an educational institution. This document is usually available upon request by the learner and sent directly to third parties (other educational institutions or employers) in order to provide a verified summary of a learner's educational experience.

So, what's an extended transcript, and how is it different from a traditional transcript?

### <a name=""></a> What's an extended transcript?

While a transcript is useful for verifying a learner's educational background, it doesn't say much about the learner's journey. What material was covered in a given course? What assessments were used? What was the course's relationship to a program or degree? What skills did a learner demonstrate, and in what areas is the learner strong or still growing?

The Extended Transcript standard defines a data model and service for institutions to provide details about learner achievements. It provides additional granularity to traditional transcripts, offering institutions the ability to recognize achievements beyond course and degree completion.

The standard supports (but doesn't presume) competency-based education (CBE). The Extended Transcript standard supports competencies, each of which may have complex relationships with other competencies. A transcript can represent anything from a flat list of skills to a complex ontology of competencies with alignments to other competency standards, and the institution can express a range of proficiency levels and outcomes.

Beyond the competency model, an extended transcript can include information about courses and degree programs, as well as assessments, certificates, and extracurriculars. Additionally, it provides a catch-all achievement type, and the data model is extensible. All of these types may have explicit relationships, and may even reference evidence.

The Extended Transcript standard supports interoperability with other IMS standards, such as Learning Information Systems (LIS) and the new Competencies & Academic Standards Exchange (CASE). An extended transcript can contain references to hosted badge assertions from the Open Badges standard. (Futhermore, the transcript itself can appear within a badge assertion in order to make the transcript itself verifiable!)

Due to its rich data model and interoperability with other standards, the Extended Transcript standard has a lot of potential in terms of integrating systems. Transcript clients can fetch transcripts in order to show learners, employers, and advisors different views of learner progress and achievements. It can also be used by the learner to share a collection badges with a badge displayer, or it can be used by employers and educational partners to match learners with professional opportunities. One day, it could even be used by institutions to automatically recognize prior educational achievements.

## <a name=""></a> In this tutorial

We're going to learn about the transcript data model by creating a progressively-complex transcript from scratch!

While you do so, I encourage you to review your transcript by uploading it to the [IMS Extended Transcript Viewer](http://projects.imsglobal.org/eT-viewer/). Before we get started, take a few minutes to look at the existing sample transcripts.

<table class="image">
<caption align="bottom">The [IMS Extended Transcript Viewer](http://projects.imsglobal.org/eT-viewer/). You can either upload an transcript or view one of the samples.</caption>
<tr><td><img src="images/1.png" width="576" height="360" /></td></tr>
</table>

<table class="image">
<caption align="bottom">This is one of the predefined transcript samples. Madison is enrolled in a fictional institution, CBU, and has attended two computer science programs.</caption>
<tr><td><img src="images/2.png" width="576" height="360" /></td></tr>
</table>

Note that the Extended Transcript standard does not prescribe what a transcript looks like, or how a transcript viewer should behave. Learning Objects created this viewer for the IMS community (and since then, other members have contributed!) in order to encourage adoption and demonstrate how the standard works, but other transcript viewers may look very different, perhaps omitting some types of data or displaying relationships differently.

<table class="image">
<caption align="bottom">Same transcript as above, but displayed in the <a href="http://learningobjects.com/#/">Learning Objects</a> transcript viewer. In this screenshot, the viewer is configured to only display  competencies.</caption>
<tr><td><img src="images/3.png" width="576" height="360" /></td></tr>
</table>

<table class="image">
<caption align="bottom">Same sample and viewer, but this time the viewer is configured to display courses. While the Extended Transcript standard provides a data model, it does not prescribe how a transcript should appear or what it must contain.</caption>
<tr><td><img src="images/4.png" width="576" height="360" /></td></tr>
</table>

## <a name=""></a> Your first transcript!

All you need it a text editor. If you use a Mac, you can use TextEdit (under "Format" menu, select "Make Plain Text"), and if you use MS Windows, you can use Notepad. I'm using [Atom Editor](https://atom.io/), and there are plenty of other open source options out there.

While knowledge of [JSON](https://www.json.org/) is a plus, no previous programming or web development experience is required.

### <a name=""></a> About JSON-LD

Before we start, you might have heard that the Extended Transcript standard uses [JSON-LD](https://json-ld.org/). (It does!) You might have heard things about JSON-LD that make it sound technically or conceptually difficult, but no need to worry: except as indicated in this tutorial, you don't need to do anything special outside to support it. As long as you follow the outlined instructions, you can create and read extended transcripts without knowing anything about JSON-LD.

Which is great, because if future you (or one of your consumers) does care about linked data, you'll be able to leverage its JSON-LD capabilities. And meanwhile, IMS already has plans that will leverage JSON-LD. (E.g., to enable verifiable transcripts using badge extensions.)

### <a name=""></a> Minimal example

Open your text edit, and create a new file: `my-first-transcript.json`

Add the following to the file and save it:

```json
{
  "@context": "https://purl.imsglobal.org/ctx/extended-transcript/v1p0",
  "id": "urn:uuid:f95fe190-9f8d-4576-85c3-7bdfb892ce5c",
  "type": "ExtendedTranscript",
  "createdAt": "2017-12-04T00:00:00.00Z",
  "issuer": {
    "id": "urn:uuid:618374e0-e761-4ccb-813a-db66e1d08310",
    "type": "Issuer",
    "name": "Mars University",
    "url": "http://example.org/mars-u"
  },
  "person": {
    "id": "urn:uuid:de15d276-a85d-4341-ba3b-d1fb86fed22c",
    "type": "Person",
    "fullName": "Amy Wong",
    "givenName": "Amy",
    "familyName": "Wong"
  },
  "records": [],
  "transcriptEntities": {
    "id": "urn:uuid:9a065540-5fc8-4fed-9dc1-a28ad51e8ee8",
    "type": "TranscriptEntitySet"
  }
}
```

Go ahead an upload it to the [IMS Extended Transcript Viewer](http://projects.imsglobal.org/eT-viewer/)

<table class="image">
<caption align="bottom">Our minimal extended transcript.</caption>
<tr><td><img src="images/5.png" width="576" height="360" /></td></tr>
</table>

Let's break this down. Here's what the transcript is telling us:
* This transcript was created on Dec 12, 2017
* It was issued by Mars University
* The learner is Amy Wong

What about the other data?

```
{
  "@context": "https://purl.imsglobal.org/ctx/extended-transcript/v1p0",
  ...
}
```

Tells us that this document should conform to Extended Transcript version 1.0 standard.

```
{
  ...
  "id": "urn:uuid:f95fe190-9f8d-4576-85c3-7bdfb892ce5c",
  ...
}
```

Gives the transcript an identifier. While you may not need this value, a consumer might. Regardless, you need to include it.

Note that as we evolve our example, almost everything in the transcript will also contain an `id`, and we will frequently used these values to establish relationships.

You may wonder: why is the ID so long? We're using [data URLs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs). Without getting into the weeds, it is better to use data URLs for JSON-LD interoperability, but you can get by with numeric identifiers (`1`, `2`, etc) for purposes of this tutorial.

```
{
  ...
  "type": "ExtendedTranscript",
  ...
}
```

Declares that the object is a transcript.

(*Technical aside*: the entire data model is monomorphic, in the sense that the type of data appearing anywhere in the document is always predictable without referencing a `type` value. However, we include the `type` property because it is required by JSON-LD, but it also makes the JSON document more human readable. It also enables better error messaging.)

Go ahead and try adding some more fields to your user and issuer:

```
{
  ...
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
  ...
}
```

As a bonus, try adding a `logo` to issuer. (Hint: you'll need a URL to a web-accessible logo. If you get stuck, look at the examples in the IMS Extended Transcript Viewer; you can access their source via the "Source" link after selecting the transcript.)

### <a name=""></a> Adding a competency

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
        "name": "Harnessing Planentary Rotational Energy"
      }
    ]
  }
}
```

After saving your change, go ahead and upload it to the IMS Extended Transcript Viewer. What do you see?

Interesting, nothing happened. Where's the competency?

In the Extended Transcript Standard, there's a distinction between transcript entities and records. What we just accomplished is describing that there is a competency, "Harnessing Planentary Rotational Energy"; however, we didn't declare anything about whether the learner achieved mastery of the competency.

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
        "name": "Harnessing Planentary Rotational Energy"
      }
    ]
  }
}
```

A few things to note:
* The value of `date` indicates that the record was last updated on Nov 1, 2017.
* The value of `result` is `"Mastered"`; we're declaring that Amy mastered the referenced competency.
* Both the `Competency`'s `id` and the `TranscriptEntityLink`'s `entityId` have the same value, `"urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C"`. This is how a record references a transcript entity.

(Technical aside: `result` has an open vocabulary; there are no restrictions on what values you can set to result, as long as it is a string.)

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
        "name": "Harnessing Planentary Rotational Energy"
      }
    ]
  }
}
```

You should see something this:

<table class="image">
<caption align="bottom">Our transcript should now have one competency in it.</caption>
<tr><td><img src="images/6.png" width="576" height="360" /></td></tr>
</table>

What if Amy is still working on this competency? This this:

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

### <a name=""></a> Adding another competency

Say "Harnessing Planentary Rotational Energy" is part of a higher level competency, "Alternative Energy". To express this in the transcript, we're going to need to add the new transcript entity, add the record for the learner, and somehow associate the two.

First, let's add the transcript entity:

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
        "name": "Harnessing Planentary Rotational Energy"
      },{
        "id": "urn:uuid:b2c3235a-49a5-4222-aba9-80c960cb832e",
        "type": "Competency",
        "name": "Alternative Energy"
      }
    ]
  }
}

```

If you save the file and upload it, you will see that nothing has changed. Again, the transcript entities describe possible achievement objects, but they do not suggest that a learner has actually done something.

Second, let's add another record:

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
    },{
      "id": "urn:uuid:ac10a029-05e7-4364-8521-97c3a4018388",
      "type": "Record",
      "date": "2017-11-01T00:00:00.000Z",
      "result": "Mastered",
      "recordOf": {
        "id": "urn:uuid:c8d04637-c503-455a-b1d8-826f1e23eb7f",
        "type": "TranscriptEntityLink",
        "entityType": "Competency",
        "entityId": "urn:uuid:b2c3235a-49a5-4222-aba9-80c960cb832e"
      }
    }
  ],
  ...
}
```

We have one more step, but before we take that step, save your changes and upload the transcript to the IMS Extended Transcript Viewer. You should see two competencies.

<table class="image">
<caption align="bottom">Our transcript should now have two competencies.</caption>
<tr><td><img src="images/7.png" width="576" height="360" /></td></tr>
</table>

### Associating the competencies

Third, let's declare that "Alternative Energy" is the parent of "Harnessing Planentary Rotational Energy":

```
{
  ...,
  "transcriptEntities": {
    "id": "urn:uuid:98f56753-973d-4c2d-865a-f567c9896ed7",
    "type": "TranscriptEntitySet",
    "competencies": [
      {
        "id": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C",
        "type": "Competency",
        "name": "Harnessing Planentary Rotational Energy"
      },{
        "id": "urn:uuid:b2c3235a-49a5-4222-aba9-80c960cb832e",
        "type": "Competency",
        "name": "Alternative Energy",
        "associations": [
          {
            "id": "urn:uuid:7aade551-fbc8-44b5-8b96-036632858117",
            "type": "Association",
            "entityType": "Competency",
            "entityId": "urn:uuid:D2986DEB-AF8D-42B9-9E29-E64784B9E12C",
            "associationType": "isParentOf"
          }
        ]
      }
    ]
  }
}
```

Note that the `Association`'s `entityId` matches the `id` for the "Harnessing Planetary Rotational Energy" competency. Similar to how records reference entities, this is how we relate entities to other entities.

Save the changes and upload it to the viewer.

<table class="image">
<caption align="bottom">The competencies are now related via a parent-child association.</caption>
<tr><td><img src="images/8.png" width="576" height="360" /></td></tr>
</table>

Alternatively, we could have declared that "Harnessing Planentary Rotational Energy" is the child of "Alternative Energy" using the `"isChildOf"` type. Can you figure out how?

There are a total of ten available association types, though you will probably mostly use `"isParentOf"` or `"isChildOf"`. Any transcript entity may have an association with any association type with any other transcript entities, though the provider is responsible for generating meaningful transcripts. (E.g., don't generate a transcript where A is parent of B, which is parent of A.)

To learn more about available associations, see the [AssocationType Vocabulary Description](https://www.imsglobal.org/sites/default/files/ExtendedTranscript/etv1p0candidatefinal/ET-InformationModel/ETServiceGroup_InfoModel.html#Enumerated_AssociationType) section within the Extended Transcript Service Information Model documentation.

### <a name=""></a> Adding a degree program and a course

Let's wrap up this tutorial by adding a couple more transcript entity types.

Amy is working on her PhD in Applied Physics, and she took a course in applied alternative energies:

```
{
  ...,
  "transcriptEntities": {
    "competencies": [
      ...
    ],
    "courses": [
      {

      }
    ],
    "degrees": [
      {

      }
    ]
  }
}
```
