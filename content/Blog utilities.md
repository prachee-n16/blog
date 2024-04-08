This blog was built with Obsidian and Quartz.

To see what this blog looks like locally,

```bash
npx quartz build --serve --port 8000
```

There are some defaults that can be overriden with flags, view list using `npx quartz build --help`

To sync the content to upload to repository,

```bash
npx quartz sync --no-pull
```

Some common fields to set on notes:

- `title`: Title of the page. If it isn’t provided, Quartz will use the name of the file as the title.
- `description`: Description of the page used for link previews.
- `aliases`: Other names for this note. This is a list of strings.
- `tags`: Tags for this note.
- `date`: A string representing the day the note was published
- `draft`: Whether to publish the page or not.