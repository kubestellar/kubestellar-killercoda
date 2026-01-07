# Contributing

## About This Repo

This repo provides interactive scenarios for [Killercoda](https://killercoda.com), a platform that runs browser-based labs.

## Killercoda Structure

Each scenario is a directory under `scenarios/` with:

```
scenario-name/
├── index.json       # Config: title, steps, backend image
├── intro.md         # Shown before step 1
├── finish.md        # Shown after last step
└── step1/
    └── text.md      # Step instructions (markdown)
```

**Key points:**
- Killercoda reads `index.json` to build the UI
- `text.md` files contain the actual instructions users see
- Code blocks with `{{copy}}` or `{{exec}}` become clickable
- Backend `imageid` determines the VM (`ubuntu` is used)

See [Killercoda docs](https://killercoda.com/creators) and [examples](https://github.com/killercoda/scenario-examples).

## Testing Locally

Killercoda pulls from git branches. To test:

1. Push your branch to this repo
2. Add repo to your [Killercoda account](https://killercoda.com/creator/repository)
3. Killercoda auto-updates on push
4. Run scenario at `killercoda.com/<your-username>/<repo-name>`

**Note:** Can't test Killercoda scenarios purely locally - need the platform.

## Current Status

`kubestellar-getting-started` scenario has structure + commands but needs testing.

**Blockers marked with TODO:**
- Confirm install commands work in Killercoda ubuntu image
- Capture actual cluster/namespace/context names from install
- Document expected outputs

See [NOTES.md](NOTES.md) for testing checklist.

## Making Changes

**Before editing steps:**
- Commands must match [KubeStellar docs](https://kubestellar.io/docs)
- Test in actual Killercoda environment before removing TODOs
- Update NOTES.md checklist as you complete items

**File changes:**
- `step*/text.md` - user-facing instructions
- `index.json` - step titles, description, backend
- `intro.md` / `finish.md` - scenario start/end

## Common Tasks

**Add a new step:**
1. Create `stepN/text.md`
2. Add step entry to `index.json` steps array
3. Test in Killercoda

**Change commands:**
1. Update `text.md` with new commands
2. Verify against official docs
3. Add TODO if output needs confirmation

**Complete a TODO:**
1. Test in Killercoda
2. Document actual output/behavior
3. Remove TODO comment
4. Check off item in NOTES.md
