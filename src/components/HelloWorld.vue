<script setup>

</script>

<template>
<h1 id="bank_title">Banking App</h1>
<div id="balance_info">
<p>Please enter your starting balance below</p>
<form id="balance_form">
Checking Balance:<b/>
<input type="number" name="checking_balance" id="checking_balance" class="enter_balance"><br/>
Savings Balance:<br/>
<input type="number" name="savings_balance" id="savings_balance" class="enter_balance"><br/><br/>
<input type="button" value="Submit" id="submit_value" form="balance_form">
</form>
</div>
<div class="row">
<div class="bank" id="checking_info">
<h2>Checking Account</h2>
<p id="current_checking_balance">Current Balance: </p>
<div id="enter_transaction">
<form id="transaction_form">
Amount:<br/>
<input type="number" name="transaction_description" id="transaction_description" class="transaction"><br/>
<div id="desc">
Description:<br/>
<input type="text" name="transaction_description" id="transaction_description" class="transaction"><br/>
</div>
<select name="transaction_type" id="transaction_type" class="trans_type">
<option value="Debit">Debit</option>
<option value="Deposit">Deposit</option>
<option value="Withdraw">Withdraw</option>
<option value="Transfer">Transfer</option>
</select>
<input type="button" value="Submit" id="submit_transaction"  form="transaction_form" class="submit_trans">
</form>
<br/>
</div>
<table id="trans_table">
<tr class="trans_table">
<th>Transaction</th>
<th>Description</th>
<th>Amount</th>
<th>Balance</th>
</tr>
</table>
</div>
<div class="bank" id="savings_info">
<h2>Savings Account</h2>
<p id="current_savings_balance">Current Balance: </p>
<div id="enter_transaction_savings">
<form id="transaction_form_savings">
Amount:<br/>
<input type="number" name="transaction_amount" id="transaction_amount_savings" class="transaction"><br/>
<select name="transaction_type" id="transaction_type_savings" class="trans_type">
<option value="Deposit">Deposit</option>
<option value="Withdraw">Withdraw</option>
<option value="Transfer">Transfer</option>
</select>
<input type="button" value="Submit" id="submit_transaction_savings" form="transaction_form" class="submit_trans">
</form>
<br/>
</div>
<table id="trans_table_savings">
<tr class="top_of_table">
<th>Transaction Type</th>
<th>Description</th>
<th>Amount</th>
<th>Balance</th>
</tr>
</table>
</div>
</div>
</template>

<style scoped>
.row {
  display: grid;
  grid-template-columns: repeat( auto-fit, minmax(33.33%, 1fr));
}

.bank {
  grid-column: span 1;
  background-color: #1c1917;
  border: solid;
  margin: 5px;
  padding: 100px;
  border-radius: 6px;
  -moz-border-radius:6px;
  border-color: #c4c4c4;
  color: #e5e5e5;
}

#bank_title {
  color: #1c1917;
}

#balance_info {
  display: grid;
  background-color: #2b2b2b;
  color: #e5e5e5;
  border: solid;
  margin: 5px;
  padding: 100px;
  border-radius: 6px;
  border-color: #c4c4c4;
}

.enter_balance {
  background: #F5F5F5;
  border: 1px solid #c4c4c4;
  border-radius: 5px;
  padding: 2px;
  margin: 5px;
}

#submit_balance {
  background: #F5F5F5;
  border: 1px solid #c4c4c4;
  border-radius: 5px;
  padding: 2px;
  margin: 5px;
}

table {
  border-collapse: separate;
  border: solid #c4c4c4 1px;
  border-radius: 6px;
  -moz-border-radius: 6px;
}

td, th {
  border-left: solid #c4c4c4 1px;
  border-top: solid #c4c4c4 1px;
}

th {
  background-color: #c4c4c4;
  border-top: none;
}


</style>
