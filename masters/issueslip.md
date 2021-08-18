# ISSUESLIP

This is the master ISSUESLIP for NEKLS.  All other ISSUESLIPs are based on this document.

Any of the sub-sections of #slip_library_info and #slip_borrower_info can be modified or removed based on the library's preferences.  Likewise #cost_statement can be removed by the libraries that don't want it.

```html
[% USE ItemTypes %]
[% USE KohaDates %]
[%- USE Price -%]
[% totalValue = 0 %]

<!DOCTYPE html>

<html>

<head>

  <title>Issue Slip</title>
  <!-- Notice code: ISSUESLIP; Library: master; -->

  <meta charset="UTF-8" />

</head>

<body>

  <div class="slip">



  </div>

</body>

</html>
```
