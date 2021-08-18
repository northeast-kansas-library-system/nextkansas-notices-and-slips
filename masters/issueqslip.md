# ISSUEQSLIP

This is the master ISSUEQSLIP for NEKLS.  All other ISSUEQSLIPs are based on this document.

Any of the sub-sections of #slip_library_info and #slip_borrower_info can be modified or removed based on the library's preferences.  Likewise #cost_statement can be removed by the libraries that don't want it.

```html
[% USE ItemTypes %]
[% USE KohaDates %]
[%- USE Price -%]
[% totalValue = 0 %]
[%- USE date -%]
[%- manip = date.manip -%]

<!DOCTYPE html>

<html>

<head>

  <title>Issue Quick Slip</title>
  <!-- Notice code: ISSUEQSLIP; Library: master; -->

  <meta charset="UTF-8" />

</head>

<body>

  <div class="slip">

    <div id="slip_content">

      <div id="slip_library_info">

        <div id="slip_library_name">
          <h3>[% branch.branchname %]</h3>
        </div>

        <div id="slip_library_address">
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
          <p>[% borrower.firstname %] [% borrower.surname %]</p>
        </div>

        <div id="slip_borrower_address">
          <p>
            [% borrower.address %]<br />
            [% IF borrower.address2 %][% borrower.address2 %]<br />[% END %]
            [% borrower.city %], [% borrower.state %] [% borrower.zipcode %]
          </p>
        </div>

        <div id="slip_borrower_email">
          <p>Email: [% borrower.email %]</p>
        </div>

        <div id="slip_borrower_phone">
          <p>Phone: [% borrower.phone %]</p>
        </div>

      </div>

      <div id="slip_cko">
        <h2>Checked out:</h2>
          [% FOREACH checkout IN borrower.checkouts %]
            [% IF ! checkout.is_overdue %]
              <p>
                <ins>[% checkout.item.biblio.title FILTER upper %][% IF checkout.item.biblio.subtitle %] [% checkout.item.biblio.subtitle FILTER upper | $Remove_MARC_punctuation %]</ins>[% IF checkout.item.effective_itemtype %] ([% ItemTypes.GetDescription(checkout.item.effective_itemtype) %])[% END %][% END %]<br />
                Barcode: [% checkout.item.barcode %]<br />
                Date due: [% checkout.date_due | $KohaDates %]<br />
                -----
              </p>
            [% END %]
          [% END %]
      </div>

      <div id="slip_od">
        <h2>Overdue:</h2>
          [% FOREACH checkout IN borrower.checkouts %]
            [% IF checkout.is_overdue %]
              <p>
                <ins>[% checkout.item.biblio.title FILTER upper %][% IF checkout.item.biblio.subtitle %] [% checkout.item.biblio.subtitle FILTER upper | $Remove_MARC_punctuation %]</ins>[% IF checkout.item.effective_itemtype %] ([% ItemTypes.GetDescription(checkout.item.effective_itemtype) %])[% END %][% END %]<br />
                Barcode: [% checkout.item.barcode %]<br />
                Date due: [% checkout.date_due | $KohaDates %]<br />
                ----------
              </p>
            [% END %]
          [% END %]
      </div>

      <div id="checkout_count_all">
        <p>Total items checked out: [% borrower.checkouts.count %]</p>
      </div>

      <div id="cost_statement">
        [% FOREACH checkout IN checkouts %]
          [%~ SET item = checkout.item %]
          [% totalValue = item.price + totalValue %]
        [% END %]
        [% FOREACH overdue IN overdues %]
          [%~ SET item = overdue.item %]
          [% totalValue = item.price + totalValue %]
        [% END %]

        <p>
          Cost of all items checked out:<br />
          $[% totalValue | $Price %]<br />
          Cost of using the library:<br />
          Priceless!
        </p>
      </div>

    </div>

  </div>

</body>

</html>
```
