# ISSUEQSLIP

This is the master ISSUEQSLIP for NEKLS.  All other ISSUEQSLIPs are based on this document.

Any of the sub-sections of #slip_library_info and #slip_borrower_info can be modified or removed based on the library's preferences.  Likewise #cost_statement can be removed by the libraries that don't want it.

```html

[% USE KohaDates %]
[%- USE Price -%]
[% totalValue = 0 %]
[%- USE date -%]
[%- manip = date.manip -%]

<!DOCTYPE html>

<html>

<head>

  <title>Issue Quick Slip</title>

  <meta charset="UTF-8" />

  <style type="text/css">
    * {
      font-family: Verdana, Arial, sans-serif;
    }

    body {
      color: #000000;
      background-color: #ffffff;
      width: 70mm;
      margin: 0;
    }

    p {
      font-size: 10pt;
    }

    h1 {
      font-size: 1.6em;
    }

    h2 {
      font-size: 1.5em;
    }

    h3 {
      font-size: 1.4em;
    }

    h4 {
      font-size: 1.3em;
    }

    h5 {
      font-size: 1.2em;
    }

    h6 {
      font-size: 1.1em;
    }
  </style>

</head>

<body>

  <div id="slip_contents">

    <div id="slip_library_info">

      <div id="slip_library_name">
        <h3>[% branch.branchname %]</h3>
      </div>

      <div id="slip_library_address">
        <!--- Delete this div if the library doesn't want their full address on its receipts --->
        <p>
          [% branch.branchaddress1 %]<br />
          [% IF branch.branchaddress2 %][% branch.branchaddress2 %]<br />[% END %]
          [% branch.branchcity %], [% branch.branchstate %] [% branch.branchzip %]<br />
          Ph: [% branch.branchphone %]<br />
          [% branch.branchemail %]
        </p>
      </div>

      <div id="slip_library_catalog_url">
        <p>Renew materials and place requests online: <br />
          <b><u>nextkansas.org</u></b>
        </p>
      </div>

    </div>

    <div id="slip_date">
      <h3>[% today | $KohaDates %]<br /></h3>
    </div>

    <div id="slip_borrower_info">

      <div id="slip_borrower_cardnumber">
        <p>
          Checked out to [% borrower.cardnumber %]
        </p>
      </div>

      <div id="slip_borrower_name">
        <!--- Delete/modify this div if the library doesn't want the borrower's name on its receipts --->
        <p>[% borrower.firstname %] [% borrower.surname %]</p>
      </div>

      <div id="slip_borrower_address">
        <!--- Delete/modify this div if the library doesn't want the borrower's address on its receipts --->
        <p>
          [% borrower.address %]<br />
          [% IF borrower.address2 %][% borrower.address2 %]<br />[% END %]
          [% borrower.city %], [% borrower.state %] [% borrower.zipcode %]
        </p>
      </div>

      <div id="slip_borrower_email">
        <!--- Delete/modify this div if the library doesn't want the borrower's email on its receipts --->
        <p>Email: [% borrower.email %]</p>
      </div>

      <div id="slip_borrower_phone">
        <!--- Delete/modify this div if the library doesn't want the borrower's phone on its receipts --->
        <p>Phone: [% borrower.phone %]</p>
      </div>

    </div>

    <div id="slip_cko">
      <h4>Checked out today:</h4>
        [% FOREACH checkout IN borrower.checkouts %]
          [% IF manip.UnixDate(checkout.item.checkout.issuedate, "%Y-%m-%d") == date.format(date.now, '%Y-%m-%d') || manip.UnixDate(checkout.item.checkout.lastreneweddate, "%Y-%m-%d") == date.format(date.now, '%Y-%m-%d') %]
            <p>
              <ins>[% checkout.item.biblio.title FILTER upper %][% IF checkout.item.biblio.subtitle %] [% checkout.item.biblio.subtitle FILTER upper %][% END %]</ins><br />
              Barcode: [% checkout.item.barcode %]<br />
              Date due: [% checkout.date_due | $KohaDates %]<br />
              ----------
            </p>
          [% END %]
        [% END %]
    </div>

    <div id="checkout_count_today">
      [% today_issues = 0 %]
      [% FOREACH checkout IN borrower.checkouts %]
        [% cissue_date = manip.UnixDate(checkout.item.checkout.issuedate, "%Y-%m-%d") %]
        [% crenew_date = manip.UnixDate(checkout.item.checkout.lastreneweddate, "%Y-%m-%d") %]
        [% today = date.format(date.now, '%Y-%m-%d') %]
        [% IF cissue_date == today || crenew_date == today %]
          [% today_issues = today_issues + 1 %]
        [% END %]
      [% END %]
      <p>Items checked out today: [% today_issues %]</p>
    </div>

    <div id="checkout_count_all">
      <p>Total items checked out: [% borrower.checkouts.count %]</p>
    </div>

    <div id="cost_statement">
      <!--- Delete/modify this div if the library doesn't want the cost statement on its receipts --->
      [% FOREACH checkout IN checkouts %]
        [%~ SET item = checkout.item %]
        [% totalValue = item.price + totalValue %]
      [% END %]

      <p>
        Cost of the items checked out today:<br />
        $[% totalValue | $Price %]<br />
        Cost of using the library:<br />
        Priceless!
      </p>
    </div>

  </div>

</body>

</html>

```
