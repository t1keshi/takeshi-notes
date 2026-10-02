Previous: [Home](../README.md)  

# Claude Code

# Steering long session

### 1. Scope the work first with plan mode

In plan mode, Claude does uts research in read-only mode. It reads the code, figures out what needs to change, and hands you a plan to review.

When you get that plan, actually read it. Don't skim it. The more through the plan, the fewer surprises you'll hit once Claude starts executing.

If somehting's off or missing, just ask Claude to add it where you want. Iterating on a plan is mucn faster than letting Claude run and hoping for the best, the cleaning up the mess.


### 2. Steer while Claude works

Once Claude is running, you have a few ways to keep it pointed in the right direction.

```/compact```

Compact summarizes your conversation, uses that summary as the new context, and deletes the old messages. This frees up your context window so Claude can keep koing.

The risk is that somehting important gets dropped in the summary, and Claude drifts off course.

Add instructions after the command to tell Claude how to summarize.

```/rewind```

When Claude heads down the wrong path, you don't have to prompt your way back out. Rewind takes you to your last checkpoint. Every uses prompt creates a checkpoint you can revert to. To open the menu, double tap escape on an empty prompt.

- Restore code and conversation - roll back both together  
- Restore conversation - roll back just the chat  
- Restore code - roll back just the files  
- Summarize from here - summarize everything after the checkpoint  
- Summarize up to here - summarize everything before the checkpoint

### 3. Let Claude run more autonomously

```/goal```

Goal sets a completion condition. You describe what "done" looks like, and Claude keeps working across turns until a fast evaluator confirms those conditions are met. It won't just stop the first time it thinks it's finished.

You can clear the goal: ```/goal clear```.

The evaluator only reads the transcript. So your condition has to be checkable from the output Claude actually produces, like the results of a test run.

```/loop```

Loop runs a prompt on an interval between turns, either fixed or self-paced. Use it to pull something external, lile a CI run or a deploy, and act when the state changes.

To stop a loop, just press escape.

### 4. Run parallel work with worktrees

Two Claude session fighting over the same files leads to conflicts. That's where worktrees come in. Instead of sesions stepping on each other, each one gets its own independent file tree.

Because each agent has its own tree, they can't clobber each other's changes. When a sesion exits, a clean worktree is automatically removed.

There's one helpful file to know about. A ```.worktreeinclude``` file at the repo root lists git-ignored files to copy into each worktree. This is useful for things like an environment variable file or a local config that you need in every worktree but don't want to commit to version control.
