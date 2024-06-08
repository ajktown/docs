# Patch Ritual By Default

## Overview

Sequence diagram for `AJK Town API` endpoint: `PATCH /api/v1/rituals/default`

## Notice

Although the API returns `rituals` (or plural), AJK Town only supports one ritual at a time.

And therefore the api does not support other ids, but only the default ritual id `default`

Eventually the following api `PATCH /api/v1/rituals/default` will become: `PATCH /api/v1/rituals/{id}`.


