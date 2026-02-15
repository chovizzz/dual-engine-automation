# Troubleshooting Guide

Common issues and solutions.

## Issue: Task Not Executing

**Symptoms:**
- CRON task shows as pending but never executes
- No notifications received

**Solutions:**

1. **Check state file**
   ```bash
   read memory/cron-execution-state.json
   ```
   Look for status of your time slot.

2. **Check gateway status**
   ```bash
   openclaw gateway status
   ```
   Ensure gateway is running.

3. **Check for overlapping tasks**
   - HEARTBEAT and CRON at same time may skip
   - Check `HEARTBEAT.md` time window rules

4. **Force run a task**
   ```bash
   openclaw cron run [job-id]
   ```

---

## Issue: Notifications Not Sending

**Symptoms:**
- Task completes but no Feishu notification
- "Failed to send" errors

**Solutions:**

1. **Verify channel configuration**
   - Check `channel=feishu` is in commands
   - Verify `target=chat:oc_xxx` is correct

2. **Check Feishu permissions**
   - Bot must be in the group
   - App needs message send permission

3. **Test manual send**
   ```bash
   openclaw message send --channel feishu --target chat:oc_xxx "test"
   ```

---

## Issue: Session Path Errors

**Symptoms:**
- "Session file path must be within sessions directory"
- Agent fails to start

**Solutions:**

1. **Check agent configuration**
   - Verify `agentDir` in `openclaw.json`
   - Ensure sessions directory exists

2. **For work agent (Discord)**
   ```bash
   ls -la ~/.openclaw/agents/work/sessions/
   ```

3. **Recreate sessions directory if missing**
   ```bash
   mkdir -p ~/.openclaw/agents/work/sessions
   ```

---

## Issue: Rate Limiting

**Symptoms:**
- "Rate limit exceeded" errors
- Operations temporarily blocked

**Solutions:**

1. **Wait it out**
   - Usually resolves in 5-15 minutes
   - Check specific service rate limits

2. **Reduce frequency**
   - Increase intervals between tasks
   - Batch operations instead of individual calls

3. **Check specific service:**
   - **Clawhub**: Wait 5-10 minutes
   - **Discord API**: Reduce message frequency
   - **OpenAI/Moonshot**: Check quota

---

## Issue: Content Calendar Conflicts

**Symptoms:**
- "Post already published today"
- Unable to create new content entry

**Solutions:**

1. **Check calendar status**
   ```bash
   read memory/content-calendar.md
   ```

2. **Manual update**
   Edit the calendar to mark post as completed or pending.

3. **Check for duplicates**
   - 48-hour rule prevents similar posts
   - Modify content to be distinct

---

## Issue: Browser Automation Fails

**Symptoms:**
- "Can't reach browser control service"
- Browser snapshots fail

**Solutions:**

1. **Check browser profile**
   ```bash
   openclaw browser --browser-profile openclaw status
   ```

2. **Restart browser**
   ```bash
   openclaw browser --browser-profile openclaw stop
   openclaw browser --browser-profile openclaw start
   ```

3. **Use correct CLI format**
   ```bash
   # Correct (no --action)
   openclaw browser --browser-profile openclaw snapshot
   
   # Incorrect
   openclaw browser --browser-profile openclaw --action snapshot
   ```

---

## Issue: Self-Evolution Not Working

**Symptoms:**
- No optimization reports generated
- Strategy docs not updating

**Solutions:**

1. **Check if enabled**
   - Look for `Self-Evolution: Enabled: yes` in config

2. **Check optimization tasks**
   - Should have CRON tasks at 20:30 daily
   - Check `cron list` for evolution tasks

3. **Manual trigger**
   ```bash
   openclaw cron run [optimization-job-id]
   ```

---

## Getting Help

If issues persist:

1. **Check logs**
   ```bash
   openclaw logs --follow
   ```

2. **Verify configuration**
   ```bash
   openclaw doctor
   ```

3. **Review documentation**
   - `SKILL.md` - Quick reference
   - `references/ADVANCED.md` - Detailed config
   - `references/EXAMPLES.md` - Use cases
