# SAMPLE HEADER

This file contains a master for the header for receipts.  The body ID for most receipts is #receipt which creates a conflict with some css rules.  Using !important in the css in the header solves that problem.  A copy of print_20.1513000.css is in this folder for reference.

```html

<html>

<head>

  <title>Issue Slip</title>

  <meta charset="UTF-8" />

  <style type="text/css">
    * {
      font-family: Verdana, Arial, sans-serif !important;
    }

    body {
      color: #000000;
      background-color: #ffffff;
      width: 70mm;
      margin: 0;
      font-size: 12pt;
    }

    h1 {
      font-size: 1.7em;
      color: #000000;
    }

    h2 {
      font-size: 1.6em;
      color: #000000;
    }

    * h3 {
      font-size: 1.5em !important;
      color: #000000 !important;
    }

    h4 {
      font-size: 1.4em !important;
      color: #000000 !important;
    }

    h5 {
      font-size: 1.3em;
      color: #000000;
    }

    h6 {
      font-size: 1.2em;
      color: #000000;
    }

    p {
      font-size: 10pt;
      color: #000000;
    }
    .center {
      text-align: center;
    }
    .buffer{
      padding-bottom: 12px;
    }
  </style>

</head>

<body>

<h1>Paragraph 1</h1>
<h2>Paragraph 2</h2>
<h3>Paragraph 3</h3>
<h4>Paragraph 4</h4>
<h5>Paragraph 5</h5>
<h6>Paragraph 6</h6>
<p>Paragraph</p>

<ul>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
  <li>Four</li>
  <li>Five</li>
</ul>

<ol>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
  <li>Four</li>
  <li>Five</li>
</ol>



</body>

</html>
```
