# MEMBERSHIP_EXPIRY

This is the master MEMBERSHIP_EXPIRY for Next Search Catalog.  All other MEMBERSHIP_EXPIRYs are based on this document.

-- Conditions that trigger the notice --

This notice uses css from noticesslips.css conveyed by the NoticeCSS system preference.

```html

<html>

<head>
  <title>[% branch.branchname %] - </title>
  <!-- Notice code:  MEMBERSHIP_EXPIRY; Library: master; -->

  <meta charset="UTF-8" />

</head>

<body>

  <div class="notice">

    <div id="notice_content">

      <p>[% borrower.firstname %] [% borrower.surname %]:</p>
      <p>Your library card will expire on [% borrower.dateexpiry %]. Please call us at [% branch.branchphone %] or visit us at [% branch.branchname %] to renew your account.</p>

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
