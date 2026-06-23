# Coffee Work installed

Enable the plugin and restart Hermes/Gateway if needed:

```bash
hermes plugins enable coffee-work
hermes gateway restart   # gateway users only
```

After Hermes comes back, confirm the command is registered by running `/coffee-work`
or checking the available slash commands in your current Hermes session.

Use it inside Hermes:

```text
/coffee-work Use Codex to do a read-only review of the current repository diff.
```

If you prefer direct skill installation instead of the plugin wrapper:

```bash
hermes skills install https://raw.githubusercontent.com/Dcx-swjtu/Coffee-Work/main/SKILL.md --name coffee-work
```
