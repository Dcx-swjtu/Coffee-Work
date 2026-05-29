# Coffee Work installed

Enable the plugin and restart Hermes/Gateway if needed:

```bash
hermes plugins enable coffee-work
hermes gateway restart   # gateway users only
```

Use it inside Hermes:

```text
/coffee-work Use Codex to do a read-only review of the current repository diff.
```

If you prefer direct skill installation instead of the plugin wrapper:

```bash
hermes skills install https://raw.githubusercontent.com/Dcx-swjtu/Coffee-Work/main/SKILL.md --name coffee-work
```
