# Markdown in Sphinx

While Read the Docs allows us to use Sphinx or Mkdocs to generate the documentation, I concluded after many tests that it's better to use Sphinx. Mkdocs handling is a latter addition and is not perfectly supported, I encountered many issues and some functionnalities are disabled when using it.

But Markdown is still an easier and more popular format than Sphinx's reStructuredText.

Recently, ReadTheDocs added CommonMark support through Sphinx : http://blog.readthedocs.com/adding-markdown-support/ .

Unfortunately, CommonMark is missing a lot of useful formatting functions compared to the Github flavored Markdown. For example, if we want to create a table like this :

| Tables        | Are           | Cool  |
| ------------- | ------------- | ----- |
| value 1       | value 2       | $1600 |
| value 3       | value 4       |   $12 |
| value 5       | value 6       |    $1 |

With Github flavored Markdown we would do it like this :

```
| Tables        | Are           | Cool  |
| ------------- | ------------- | ----- |
| value 1       | value 2       | $1600 |
| value 3       | value 4       |   $12 |
| value 5       | value 6       |    $1 |
```

But with CommonMark we would have to write HTML code to have the same result (and still we would need to manually add style) :

```
<table>
  <tr>
    <th>Tables</th>
    <th>Are</th>
    <th>Cool</th>
  </tr>
  <tr>
    <td>value 1</td>
    <td>value 2</td>
    <td>$1600</td>
  </tr>
  <tr>
    <td>value 3</td>
    <td>value 4</td>
    <td>$12</td>
  </tr>
  <tr>
    <td>value 5</td>
    <td>value 6</td>
    <td>$1</td>
  </tr>
</table>
```

The good news is that there is another clever way to use Markdown in Sphinx, I found an example on how to do so here : https://github.com/mctenshi/sphinx-markdown-sample

Basically the idea is to use Pandoc (which is included in Read The Docs) to convert the Markdown files to reStructuredText files before building the documentation. This works pretty well because everything that can be done in Markdown can be done in reStructuredText (the opposite is not true).

In order to configure Read the Docs to do this, we have to add the *lib* folder containing the *sphinxcontrib_markdown.py* file at the same level than the *conf.py* file. Then we need to add this to the *conf.py* file :

```
sys.path.insert(0, os.path.abspath('.'))
sys.path.insert(0, os.path.abspath('./lib'))

extensions += ["sphinxcontrib_markdown"]

# The suffix of source filenames.
source_suffix = '.md'

markdown_title = 'The title of your documentation'
```

After this, you'll be able to use Markdown in Sphinx and enjoy all of the functionalities of Read the Docs.
