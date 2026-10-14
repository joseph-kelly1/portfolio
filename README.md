# Joseph Kelly Portfolio

Static one-page portfolio. The public web root is `public/`. Everything in it is served as is, with no build step.

## Preview locally

```sh
python3 -m http.server 8000 --directory public
```

Then open http://localhost:8000.

## Layout

- `public/index.html`: page content (the authoritative copy of visible text)
- `public/styles.css`: styles
- `docs/`: content brief, decisions, QA notes
- `resume/resume-portfolio.tex`: résumé source, kept outside the web root
