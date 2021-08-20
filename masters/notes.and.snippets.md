# Notes and snippets for notices and slips

## Add a scannable barcode number to a slip in barcode 3 of 9


``` html

<img src="/cgi-bin/koha/svc/barcode?barcode=*[% checkout.item.barcode %]*&type=Code39"></img>

```


## Quick HTML sample for issue quick slip

``` html

<html>

<head>

  <title>Issue Slip</title>

  <style type="text/css">
    /* Koha forces a #receipt id onto all pages in this template, so the "!important" tags are needed to prevent the default css for #receipt from interfering with the style for this notice */

    * {
      font-family: Verdana, Arial, sans-serif;
    }

    body {
      color: #000000 !important;
      background-color: #ffffff;
      width: 70mm;
      margin: 0;
      font-size: 10pt;
    }

    p {
      font-size: 10pt !important;
      color: #000000 !important;
    }

    h1 {
      font-size: 1.6em !important;
      color: #000000 !important;
    }

    h2 {
      font-size: 1.5em !important;
      color: #000000 !important;
    }

    h3 {
      font-size: 1.4em !important;
      color: #000000 !important;
    }

    h4 {
      font-size: 1.3em !important;
      color: #000000 !important;
    }

    h5 {
      font-size: 1.2em !important;
      color: #000000 !important;
    }

    h6 {
      font-size: 1.1em !important;
      color: #000000 !important;
    }
  </style>

</head>

<body>

<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
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

# Template Toolkit Notes

## Information about a borrower's home branch

This was information derived from a conversation on Slack with Lucas at Bywater Solutions and is set to produce single lines.

``` html

[% USE Branches %]

[% FOREACH b IN Branches.all() %]

  [% SET thisborrower_branchcode = borrower.branchcode %]

    [% IF b.branchcode == thisborrower_branchcode %]
    [% b.branchcode %]<br />
    [% b.branchname %]<br />
    [% b.branchaddress1 %]<br />
    [% b.branchaddress2 %]<br />
    [% b.branchaddress3 %]<br />
    [% b.branchzip %]<br />
    [% b.branchcity %]<br />
    [% b.branchstate %]<br />
    [% b.branchcountry %]<br />
    [% b.branchphone %]<br />
    [% b.branchfax %]<br />
    [% b.branchemail %]<br />
    [% b.branchreplyto %]<br />
    [% b.branchreturnpath %]<br />
    [% b.branchurl %]<br />
    [% b.issuing %]<br />
    [% b.branchip %]<br />
    [% b.branchnotes %]<br />
    [% b.opac_info %]<br />
    [% b.geolocation %]<br />
    [% b.marcorgcode %]<br />
    [% b.pickup_location %]<br />

  [% END %]

[% END %]

```

## Information about a checked out item's home branch

``` HTML

[% USE Branches %]

[% FOREACH checkout IN borrower.checkouts %]

  [% FOREACH b IN Branches.all() %]

    [% SET thisitem_branchcode = checkout.item.homebranch %]

      [% IF b.branchcode == thisitem_branchcode %]
      [% b.branchcode %]<br />
      [% b.branchname %]<br />
      [% b.branchaddress1 %]<br />
      [% b.branchaddress2 %]<br />
      [% b.branchaddress3 %]<br />
      [% b.branchzip %]<br />
      [% b.branchcity %]<br />
      [% b.branchstate %]<br />
      [% b.branchcountry %]<br />
      [% b.branchphone %]<br />
      [% b.branchfax %]<br />
      [% b.branchemail %]<br />
      [% b.branchreplyto %]<br />
      [% b.branchreturnpath %]<br />
      [% b.branchurl %]<br />
      [% b.issuing %]<br />
      [% b.branchip %]<br />
      [% b.branchnotes %]<br />
      [% b.opac_info %]<br />
      [% b.geolocation %]<br />
      [% b.marcorgcode %]<br />
      [% b.pickup_location %]<br />

    [% END %]

  [% END %]

[% END %]

```


## I

``` HTML

[% USE Branches %]

[% FOREACH o IN overdues %]

  [% FOREACH b IN Branches.all() %]

    [% SET thisitem_branchcode = overdue.item.homebranch %]

      [% IF b.branchcode == thisitem_branchcode %]
      [% b.branchcode %]<br />
      [% b.branchname %]<br />
      [% b.branchaddress1 %]<br />
      [% b.branchaddress2 %]<br />
      [% b.branchaddress3 %]<br />
      [% b.branchzip %]<br />
      [% b.branchcity %]<br />
      [% b.branchstate %]<br />
      [% b.branchcountry %]<br />
      [% b.branchphone %]<br />
      [% b.branchfax %]<br />
      [% b.branchemail %]<br />
      [% b.branchreplyto %]<br />
      [% b.branchreturnpath %]<br />
      [% b.branchurl %]<br />
      [% b.issuing %]<br />
      [% b.branchip %]<br />
      [% b.branchnotes %]<br />
      [% b.opac_info %]<br />
      [% b.geolocation %]<br />
      [% b.marcorgcode %]<br />
      [% b.pickup_location %]<br />

    [% END %]

  [% END %]

[% END %]

```
