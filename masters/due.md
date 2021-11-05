# DUE

This is the master DUE for Next Search Catalog.  All other DUE are based on this document.

This notice is sent to a borrower if they have "Item due" "Email" checked in their messaging preferences on the day that an item is due.  A separate email will be sent to the borrower for each item they have due.

```html
<html>

<head>
  <title>[% branch.branchname %] -Library item due today</title>
  <!-- Notice code:  DUE; Library: All -->

  <meta charset="UTF-8" />

  <style>
    * {
      font-family: Verdana, Arial, sans-serif;
    }

    body .notice {
      color: #000000;
      background-color: #ffffff;
      width: 90%;
      margin: 0;
      font-size: 12pt;
    }

    .notice p {
      font-size: 12pt;
      color: #000000;
    }

    .notice h1 {
      font-size: 1.6em;
      color: #000000;
    }

    .notice h2 {
      font-size: 1.5em;
      color: #000000;
    }

    .notice h3 {
      font-size: 1.4em !important;
      color: #000000;
    }

    .notice h4 {
      font-size: 1.3em !important;
      color: #000000;
    }

    .notice h5 {
      font-size: 1.2em;
      color: #000000;
    }

    .notice h6 {
      font-size: 1.1em;
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

  <div class="notice">

    <div id="notice_content">

      <h3 class="buffer">*Please respond to this automated message by phoning [% branch.branchphone %]*</h3>
      <h2>[% branch.branchname %] - Library item due today</h2>
      <p>The following item is due at the library today.  This item is checked out to your library card number ending in [% borrower.cardnumber.substr(-6) FILTER upper %].</p>
      <p>The details are as follow:</p>
      <item>
        <p><<items.content>></p>
      </item>
      <p>If you have returned this item recently, or if you believe this email was sent to you in error, please contact us at <strong><ins>[% branch.branchphone %]</ins></strong>.</p>

    </div>

    <footer>

      <p>Thank you,</p>
      <p>
        [% branch.branchname %]<br />
        [% branch.branchaddress1 %]<br />
        [% branch.branchcity %], [% branch.branchstate %] [% branch.branchzip %]
      </p>
      <p>You can access your account on-line at <a href="https://nextkansas.org">https://nextkansas.org</a> 24 hours a day.</p>
      <p>Visit our library's website at: <a href="[% branch.branchurl %]">[% branch.branchurl %]</a></p>
      <p>If you no longer wish to receive these e-mails or if you have any questions, please contact us by phone at <strong><ins>[% branch.branchphone %]</ins></strong>.</p>

    </footer>

  </div>

</body>

</html>


```
