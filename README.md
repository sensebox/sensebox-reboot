# sensebox.github.io

This Repo holds the new senseBox website.

## Editing the website

Most of the articles and press releases are written with [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). HTML can be used if needed, e.g. for linking to external pages or for embedding images.

### Adding blog posts
[Here you can see how to add a new blog post](how-to-add-blog-post.md)

### Adding events

Add the event as a markdown file in the `_events` folder. Follow the same schema as existing files.

### Adding new Projects

Add the new projects a a markdown file in the `_projects` folder. Use the template and follow the same schema as existing files.

### Adding press reports

Add the award as a markdown file in the format `2015-01-01-topic.md` in the `_press` folder. Follow the same schema as existing files.

### Adding awards

Add the press report as a markdown file in the `_awards` and `_awards_en` folder. Follow the same schema as existing files.

### Adding team members biographies

Add the biography as a markdown file in the format `name.md` in the `_team` folder. Follow the same schema as existing files.


### File structure
- `_awards_de`: Awards won by senseBox written in german
- `_awards_en`: Awards won by senseBox written in english
- `_data`:
  - `i18n`: Main folder for translations
    - `de`: tranlations for each page in german
    - `en`: tranlations for each page in english
- `_events`: Upcoming envents where senseBox will attend
- `_includes`:
  - `_pages`: content for each page
  - footer, header etc...
- `_layouts`: default page layout
- `_posts`: blog posts
- `_projects`: project pages
- `_press`: press articles
- `_sass`: sass stylesheets
- `assets`: .js scripts
- `bower_components`: bower components
- `css`: css stylesheets
- `docs`: data like pdf...
- `en`: english pages (includes pages from `_includes/_pages`)
- `images`: used images
- german pages (includes pages from `_includes/_pages`)
- favicon
- readme
- ...


## Running the page locally with Jekyll

Clone repository, `cd` into it and run:

```bash
bundle instal
bundle exec jekyll serve
```

In a Vagrant environment, run:

```bash
jekyll serve --host 0.0.0.0 --force_polling
```
