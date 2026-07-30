# Data Model

> MemoryClip Data Model
>
> Version 1.0
>
> Everything is a Memory Graph.

---

# Overview

MemoryClip is not organized around videos.

It is organized around people.

Every documentary is generated from structured knowledge.

```
Project

↓

Person

↓

Memory Graph

↓

Documentary
```

Unlike traditional editors,

MemoryClip stores knowledge instead of timelines.

---

# Design Principles

The data model follows several rules.

## Person Centric

Everything belongs to one or more people.

Never organize around files.

---

## Evidence Driven

Every fact must have evidence.

Facts never exist independently.

---

## Graph Native

Relationships are first-class citizens.

Person

↓

Parent

↓

School

↓

Career

↓

Marriage

↓

Children

↓

Legacy

---

## Immutable Assets

Original uploads are never modified.

Processing creates new versions.

---

## Versioned Knowledge

Biographies

Timelines

Stories

Documentaries

all support version history.

---

# Top Level Model

```
Workspace
    │
    ├── Projects
    │
    └── Users
```

---

# Workspace

A workspace represents one organization.

Examples

Family

Museum

Library

Archive

University

Funeral Service

Historical Institution

```
Workspace

id

name

owner

members

settings
```

---

# Project

A project is one documentary project.

```
Project

id

title

description

status

owner

createdAt

updatedAt
```

Relationships

```
Project

↓

Persons

Assets

Timeline

Stories

Documentaries

Comments

Versions
```

---

# Person

The most important entity.

```
Person

id

fullName

birthDate

deathDate

gender

occupation

religion

nationality

biography

summary

avatar

confidence
```

Every documentary starts from a Person.

---

## Person Profile

Additional attributes

```
Aliases

Nicknames

Education

Military

Career

Awards

Languages

Hobbies

Residence

Organizations

Religion

Political Affiliation

Military Unit
```

Everything optional.

---

# Relationship

```
Relationship

id

sourcePerson

targetPerson

type

confidence

evidence
```

Supported types

Parent

Child

Sibling

Spouse

Friend

Teacher

Student

Coworker

Commander

Served With

---

# Family

```
Family

id

surname

description

members
```

Supports multiple generations.

---

# Asset

Everything uploaded becomes an Asset.

```
Asset

id

type

owner

storageKey

hash

mimeType

createdAt

metadata
```

---

Supported Types

```
Photo

Video

Audio

Document

Letter

Diary

Certificate

Passport

Military Record

Gravestone

Portrait

Generated Image

Generated Video
```

---

# Asset Metadata

Example

```
Photo

↓

Camera

Date

GPS

Faces

Objects

Resolution

Orientation

Embedding

Color Profile
```

---

# Asset Version

```
Original

↓

Restored

↓

Colorized

↓

Upscaled

↓

Animated
```

Each version has

```
versionId

parentVersion

algorithm

createdAt
```

Original remains immutable.

---

# Evidence

Evidence connects facts with assets.

```
Evidence

id

assetId

page

boundingBox

speaker

timestamp

confidence
```

Example

Birth Date

↓

Gravestone OCR

↓

Confidence 99%

---

# Place

```
Place

id

name

country

region

city

latitude

longitude

historicalName
```

One place may change names over history.

---

# Timeline Event

Canonical historical unit.

```
TimelineEvent

id

title

date

datePrecision

description

location

people

assets

evidence

confidence
```

Examples

Born

Marriage

Graduation

Military Service

Immigration

Retirement

Death

---

# Historical Event

Separate from personal events.

```
HistoricalEvent

id

title

period

country

summary

references
```

Example

World War II

Vietnam War

Great Depression

Moon Landing

Personal events may reference historical events.

---

# Biography

Biography is structured.

```
Biography

id

person

chapters

summary

language

style

version
```

Sections

Early Life

Education

Career

Marriage

Achievements

Later Life

Legacy

---

# Story

Story is generated from Biography.

```
Story

id

theme

tone

style

outline

chapters
```

Styles

Documentary

Family

Historical

Museum

Educational

---

# Documentary

Top level production.

```
Documentary

id

project

title

duration

language

aspectRatio

status
```

Contains

```
Chapters

Scenes

Shots

Subtitles

Narration

Music

Credits
```

---

# Chapter

```
Chapter

id

title

summary

timelineEvents

order
```

---

# Scene

```
Scene

id

chapter

duration

goal

assets

prompt

voice
```

---

# Shot

Smallest visual unit.

```
Shot

id

scene

camera

duration

transition

prompt

assets
```

---

# Narration

```
Narration

id

scene

text

language

voice

duration
```

---

# Subtitle

```
Subtitle

id

scene

language

start

end

text
```

---

# Music Track

```
Music

id

style

emotion

duration

license
```

---

# Comment

Supports collaboration.

```
Comment

id

user

target

message

createdAt
```

Target may be

Biography

Scene

Timeline

Asset

Person

---

# Task

Agents work through tasks.

```
Task

id

agent

type

status

input

output
```

Examples

OCR

Biography

Timeline

Story

Render

Export

---

# Agent

```
Agent

id

name

role

model

tools

status
```

Examples

Memory Agent

Historian Agent

Director Agent

Composer Agent

---

# Render Job

```
RenderJob

id

documentary

progress

status

resolution

output
```

---

# Export

```
Export

id

format

quality

destination

checksum
```

Formats

MP4

MOV

WebM

Interactive HTML

Museum Package

---

# Audit Log

Everything is recorded.

```
AuditLog

id

user

action

target

timestamp
```

Supports

Compliance

Recovery

Collaboration

---

# Version History

Every important object supports versioning.

```
Biography v1

↓

Biography v2

↓

Biography v3
```

Likewise

Timeline

Story

Documentary

Asset Metadata

Knowledge Graph

---

# Memory Graph

Everything ultimately becomes a graph.

```
Project

↓

Person

↓

Timeline

↓

Events

↓

Assets

↓

Evidence

↓

Story

↓

Scenes

↓

Documentary
```

Every node references every other node.

No duplicated knowledge.

No isolated files.

Everything is connected.

---

# Entity Relationship Diagram

```
Workspace
│
├── User
│
├── Project
│   │
│   ├── Person
│   │     │
│   │     ├── Relationship
│   │     ├── Biography
│   │     ├── TimelineEvent
│   │     └── Story
│   │
│   ├── Asset
│   │     ├── AssetVersion
│   │     ├── Evidence
│   │     └── Embedding
│   │
│   ├── Documentary
│   │      ├── Chapter
│   │      ├── Scene
│   │      ├── Shot
│   │      ├── Narration
│   │      ├── Subtitle
│   │      └── Music
│   │
│   ├── AgentTask
│   └── RenderJob
│
└── AuditLog
```

---

# Design Philosophy

Traditional video editors store clips.

MemoryClip stores lives.

A documentary is not the primary asset.

The Memory Graph is.

As AI improves, new documentaries, books, interactive museums, podcasts, family archives, and digital memorials can all be regenerated from the same structured graph without ever re-uploading the original memories.
