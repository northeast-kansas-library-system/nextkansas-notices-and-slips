# ISSUESLIP

This is the master ISSUESLIP for NEKLS.  All other ISSUESLIPs are based on this document.

Any of the sub-sections of #slip_library_info and #slip_borrower_info can be modified or removed based on the library's preferences.  Likewise #cost_statement can be removed by the libraries that don't want it.

```html
[% USE ItemTypes %]
[% USE KohaDates %]
[%- USE Price -%]
[%- USE date -%]
[% totalValue = 0 %]

<!DOCTYPE html>

<html>

<head>
  <title>[% branch.branchname %] - Issue slip</title>
  <!-- Notice code:  ISSUESLIP; Library: master; -->

  <meta charset="UTF-8" />

  <style>
    @media print {
      body, p, h1, h2, h3, h4, h5, h6, a, td, .credit {
        width: 70mm;
        margin: 0;
        color: #000000 !important;
        background-color: #ffffff;
        font-weight: bold !important;
      }
    }

    * {
      font-family: Verdana, Arial, sans-serif;
    }

    body {
      font-size: 10pt;
    }

    .slip p {
      font-size: 10pt;
    }

    .slip h1 {
      font-size: 1.6em;
    }

    .slip h2 {
      font-size: 1.5em;
    }

    .slip h3 {
      font-size: 1.4em !important;
    }

    .slip h4 {
      font-size: 1.3em !important;
    }

    .slip h5 {
      font-size: 1.2em;
    }

    .slip h6 {
      font-size: 1.1em;
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

  <div class="slip">

    <div id="slip_content">

      <div id="slip_library_info">

        <div id="slip_library_name" class="buffer">
          <h3>[% branch.branchname %]</h3>
        </div>

        <div id="slip_library_address" class="buffer">
          <p>
            [% branch.branchaddress1 %]<br />
            [% IF branch.branchaddress2 %][% branch.branchaddress2 %]<br />[% END %]
            [% branch.branchcity %], [% branch.branchstate %] [% branch.branchzip %]<br />
            Ph: [% branch.branchphone %]<br />
            [% branch.branchemail %]
          </p>
        </div>

        <div id="slip_library_catalog_url" class="buffer">
          <p>Renew materials and place requests online: <br />
            <b><u>nextkansas.org</u></b>
          </p>
        </div>

      </div>

      <div id="slip_borrower_info">

        <div id="slip_borrower_name" class="buffer">
          <p>[% borrower.firstname %] [% borrower.surname %]</p>
        </div>

        <div id="slip_borrower_address" class="buffer">
          <p>
            [% borrower.address %]<br />
            [% IF borrower.address2 %][% borrower.address2 %]<br />[% END %]
            [% borrower.city %], [% borrower.state %] [% borrower.zipcode %]
          </p>
        </div>

        <div id="slip_borrower_email" class="buffer">
          <p>Email: [% borrower.email %]</p>
        </div>

        <div id="slip_borrower_phone" class="buffer">
          <p>Phone: [% borrower.phone %]</p>
        </div>

        <div id="slip_borrower_cardnumber" class="center buffer">
          <p>
            Last 6 digits of library<br />card number [% borrower.cardnumber.substr(-6) FILTER upper %]
          </p>
        </div>

      </div>

      [% IF checkouts.count %]
      <div id="slip_cko" class="buffer">
        <h4 class="buffer">Checked out:</h4>
        [% FOREACH checkout IN borrower.checkouts %]
        [% IF ! checkout.is_overdue %]
        <p>
          <ins>[% checkout.item.biblio.title FILTER upper %][% IF checkout.item.biblio.subtitle %] [% checkout.item.biblio.subtitle FILTER upper %][% END %]</ins><br />
          Item type: [% ItemTypes.GetDescription(checkout.item.effective_itemtype) %]<br />
          Barcode: [% checkout.item.barcode %]<br />
          Date due: [% checkout.date_due | $KohaDates %]<br />
          -----
        </p>
        [% END %]
        [% END %]

      </div>
      [% END %]

      [% IF overdues.count %]
      <div id="slip_od" class="buffer">
        <h4 class="buffer">Overdue:</h4>
        [% FOREACH checkout IN borrower.checkouts %]
        [% IF checkout.is_overdue %]
        <p>
          <ins>[% checkout.item.biblio.title FILTER upper %][% IF checkout.item.biblio.subtitle %] [% checkout.item.biblio.subtitle FILTER upper %][% END %]</ins><br />
          Item type: [% ItemTypes.GetDescription(checkout.item.effective_itemtype) %]<br />
          Barcode: [% checkout.item.barcode %]<br />
          Date due: [% checkout.date_due | $KohaDates %]<br />
          ----------
        </p>
        [% END %]
        [% END %]
      </div>
      [% END %]

      <div id="cost_statement">
        [% FOREACH checkout IN checkouts %]
        [%~ SET item = checkout.item %]
        [% totalValue = item.replacementprice + totalValue %]
        [% END %]
        [% FOREACH overdue IN overdues %]
        [%~ SET item = overdue.item %]
        [% totalValue = item.replacementprice + totalValue %]
        [% END %]

        <p>
          Cost of all items currently checked out:<br />
          $[% totalValue | $Price %]<br />
          Cost of using the library:<br />
          Priceless!
        </p>
      </div>

      <div id="checkout_count_all" class="center buffer">
        <p>Total items<br />checked out: [% borrower.checkouts.count %]</p>
      </div>

      <div id="slip_datestamp" class="center">
        <h4>This receipt printed on:<br />[% date.format(date.now, "%Y/%m/%d at %I:%M %p") %]</h4>
      </div>

    </div>

  </div>

</body>

</html>
```
