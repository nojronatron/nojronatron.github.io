# Python and Flask Cheatsheet

Notes and insights while interacting with Python Flask projects.

## Flask

- Web framework.
- Very popular.
- Similar to Express.
- Supports templates.
- Is a _synchronous_ framework.

## Quart

- Similar web framework to Flask.
- Is an _asynchronous_ framework.

### Routes

Define a route: `@app.route("/")`

### Templates

- Uses `%` signs as placeholder syntax identifiers.
- Uses inheritance to create templates from templates.
- Form support.

Call template from a route:

```python
...
@app.route("/about")
def about:
  return render_template("about.html")

...
```

## Extensions

Try 'PyPi Assistant' available for VS Code.

## Resources

- [Pamela Fox's Blog](https://blog.pamelafox.org/)
