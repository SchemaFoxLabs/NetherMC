# Event record format

[Back to NetherMC](../README.md) · [Event archive](https://github.com/SchemaFoxLabs/NetherMC-Archive)

This page documents the event log and organization metadata convention. It does not describe an implemented parser or contain real event records. Published event archives remain in the linked archive repository.

## Event entries

The following is a notation template, not executable code or strict JSON/YAML. Replace angle-bracket placeholders with actual values when writing a record. Choose one role and one reward representation for each entry.

```text
Event:
[YYYY-MM-DD (Import Time)] <EventName> {
  permission: <Author | Staff | Moderator | Partner>

  release_staff:
    - IGN: <in-game name>
      UUID: <required Minecraft UUID>
      profile: <required public social media or GitHub profile URL>

  server: <internal identification>

  content:
    description: <event description>
    rewards: <list of strings OR list of objects>

  duration: [<timezone>] YYYY-MM-DD HH:mm ~ YYYY-MM-DD HH:mm
  player_capacity: <integer>
  player_actual: <integer>
}
```

Repeat the event block for additional events.

| Field | Meaning |
| :--- | :--- |
| Import Time | Date the entry was added to the log, using `YYYY-MM-DD`; distinct from the event's scheduled time. |
| EventName | The event's name. |
| `permission` | The publishing role: `Author`, `Staff`, `Moderator`, or `Partner`. This records a role; it does not grant access permissions. |
| `release_staff` | Staff responsible for publishing the entry. For each person, record the in-game name, required Minecraft UUID, and required public social media or GitHub profile URL. |
| `server` | The internal server identification from the README, such as `practice`. |
| `content.description` | A description of the event. |
| `content.rewards` | A list of reward descriptions, or a list of objects when attributes such as quantity or rarity are needed. |
| `duration` | Start and end date/time with an explicit time zone. Use 24-hour time and `YYYY-MM-DD HH:mm`; identify the zone with a name such as `Asia/Shanghai` or an explicit UTC offset. |
| `player_capacity` | Maximum number of participants, recorded as a nonnegative integer. |
| `player_actual` | Actual number of participants, recorded as a nonnegative integer. Do not invent a count before it is known. |

For example, `2026-09-17` illustrates the date format only; it does not establish an event date.

### Reward representations

Simple rewards can be a list of strings. Rewards with attributes can use objects. These are placeholders, not announced rewards:

```text
rewards:
  - <reward description>

OR

rewards:
  - name: <reward name>
    quantity: <integer>
    rarity: <rarity description, if applicable>
```

## Organization metadata

```text
OrganizationMeta {
  current_partner:
    - <current partner>

  history_partner:
    - <previous partner>

  event_quantity: <integer>

  stafflist:
    - IGN: <in-game name>
      UUID: <required Minecraft UUID>
      profile: <required public social media or GitHub profile URL>
}
```

- `current_partner`: current partners associated with the records.
- `history_partner`: previous partners associated with the records.
- `event_quantity`: total number of events represented by the associated records; keep it consistent when records are added or corrected.
- `stafflist`: staff entries with the same in-game name, required UUID, and required public profile information as `release_staff`.

Keep staff references to public game identities and public profile links. Do not add private contact details or real-world identifying information. This document does not establish any actual staff roster or partnership.
