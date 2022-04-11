<head>
  <!-- Template Toolkit use statements -->

  [% USE Branches %]
  [% USE date %]
  [% USE ItemTypes %]
  [% USE KohaDates %]
  [% manip = date.manip %]
  [% USE Price %]
  [% totalValue = 0 %]


  <style>

    /* set whole page to Arial Black */
    * {
      font-family: 'Arial Black', 'Arial', sans-serif !important;
    }

    body {width: 70mm;}
    body{
      margin-top: 0px;
      margin-bottom: 0px;
      margin-right: 0px;
      margin-left: 5px;
    }

    .b-double {padding-bottom: 15px;}
    .b-triple {padding-bottom: 30px;}
    .b-quadruple {padding-bottom: 45px}
    .b-quintuple {padding-bottom: 60px}
    .b-sextuple {padding-bottom: 75px}
    .b-septuple {padding-bottom: 90px;}
    .top-one {padding-top: 1in;}
    .top-two {padding-top: 2in;}
    .top-three {padding-top: 3in;}
    .top-four {padding-top: 4in;}
    .top-five {padding-top: 5in;}
    .top-six {padding-top: 6in;}

    article{display:inline-block}
    .right{float:right}
    .slip {font-size: 110%;}
    .slip h1 {font-size: 250%;}
    .slip h2 {font-size: 150%;}
    .slip h3 {font-size: 130%;}
    .slip h4 {font-size: 120%;}
    .underline {text-decoration: underline;}
  </style>

<title>Request slip</title>

</head>

[% IF hold.branchcode != Branches.GetLoggedInBranchcode() %]

<!-- If item is on hold at another location -->

  <div id="ship-to-branch" class="slip">

    <!-- Shipped to information -->
    <h1 class="double">
      [% hold.branch.branchnotes %]
      <span class="right">

      </span>
    </h1>

    <p>Ship to:</p>
    <h3 class="double">
      <strong>
        [% hold.branch.branchname %]<br />
        [% hold.branch.branchaddress1 %]<br />
        [% hold.branch.branchcity %], [% hold.branch.branchstate %] [% hold.branch.branchzip %]
      </strong>
    </h3>

    <!-- Item information -->
    <h3 class="underline">[% biblio.title %]</h3>
    [% IF biblio.author %]<p>by: [% biblio.author %]</p>[% END %]
    <p>[% item.itemcallnumber %]</p>
    <p class="double">[% item.barcode %]</p>

    <!-- Shipped from information -->
    <p>
      Shipped from: [% Branches.GetLoggedInBranchcode() %]<br />
      shipped on: [% today | $KohaDates %]
    </p>

  </div>


[% ELSIF hold.branchcode == Branches.GetLoggedInBranchcode() && borrower.smsalertnumber || borrower.email %]

<!-- If item is on hold at this library and the borrower has an e-mail address -->

<div id="hold-here" class="slip">

  <div id="hold-for">
    <!-- Hold for name -->
    <h2 style="text-align:right">Hold until: [% hold.expirationdate | $KohaDates dateformat => 'us' | truncate (6, ' ') %]</h2>
    <h2 style="text-align:left" class="sextuple">[% borrower.surname %],  [% borrower.firstname  %]</h2>
  </div>

  <div id="iteminfo">
    <h3> ITEM ON HOLD </h3>
    <ul>
      <li>[% biblio.title %]</li>
      [% IF biblio.author %]<li>[% biblio.author %]</li>[% END %]
      [% IF item.itemcallnumber %]<li>[% item.itemcallnumber %]</li>[% END %]
      <li>[% item.barcode %]</li>
      <li>Available since: [% hold.waitingdate | $KohaDates dateformat => 'us' %]</li>
      [% IF hold.reservenotes %]<ul><li>Notes: <br />[% hold.reservenotes %]</li></ul>[% END %]
    </ul>
    <p class="top-big-space">.</p>
  </div>
</div>

[% ELSIF hold.branchcode == Branches.GetLoggedInBranchcode() %]

  <div>

    <h2 style="text-align:right" "padding-left:25px">Hold till: _________</h2>
    <h2 style="text-align:left">  [% borrower.surname  %]  [% borrower.firstname %]
    </h2>
    <br />
    <br />
    <br />

    <div id="iteminfo">
      <h3> ITEM ON HOLD </h3>
      <ul>
        <li> [% biblio.title %]  [% IF biblio.author %] // [% biblio.author %] [% END %] // [% item.itemcallnumber %] </li>
        <li>[% item.barcode %]</li>
        <li>Available Since: [% hold.waitingdate | $KohaDates dateformat => 'us' %]</li>
      <ul>
      [% IF hold.reservenotes %]
        <p>
          Notes::
          <br />
          [% hold.reservenotes %]
        </p>
      [% END %]
    </div>

    <h2>Phone Call Checklist</h2>
    <h3>
      [% borrower.firstname %] [% IF borrower.othernames %] ([% borrower.othernames %])[% END %]
    </h3>
    <p>[% borrower.phone %]</p>
    <h3>Circle one:</h3>
    <p>Spoke directly with the patron.</p>
    <p>Left message with person who answered the phone.</p>
    <p>Left message on answering machine / voice mail.</p>
    <p>
      Please send a postcard to the patron if you cannot
      <br />
      contact them by other means within 24 hours of the
      <br />
      requested item's arrival.
    </p>
  </div>

[% END %]
