<script setup>
const transactions = document.querySelector("#enter_transaction")
const transactionsSavings = document.querySelector("enter_transaction_savings");
const transactionType = document.querySelector("#transaction_type") 
const transactionTypeSavings = document.querySelector("#transaction_type_savings");
const transAmount = document.querySelector("#transaction_amount");
const transAmountSavings = document.querySelector("#transaction_amount_savings");
const transDescription = document.querySelector("#transaction_description");
const table = document.querySelector("#trans_table");
const tableSavings =  document.querySelector("#trans_table_savings");
const desc = document.querySelector("#desc");
const checkingStartingBalance = document.querySelector("#checking_balance");
const savingsStartingBalance = document.querySelector("#savings_balance");
const balanceInfo = document.querySelector("#balance_info");

// Checking Account
let checkingAccount = {
  name: "checking",
  balance: 0.00,
  allTransactions: [],
  deposit: function (amount) {
    this.balance += amount;
    this.allTransactions.push({
      type: "deposit",
      amount: amount,
    })
  },
  withdraw: function (amount) {
    this.balance -= amount;
    this.allTransactions.push({
      type: "withdrawal",
      amount: amount,
    })
  },
  debit: function (amount, purpose) {
    this.balance -= amount;
    this.allTransactions.push({
      type: "debit",
      amount: amount,
      purpose: purpose,
    });
  },
  transfer: function (amount, transferAccount) {
    this.balance -= amount;
    transferAccount.allTransactions.push({
      type: "transfer",
      amount: amount,
      purpose: "transfer",
    }),
    this.allTransactions.push({
      type: "transfer",
      amount: amount,
      purpose: "transfer",
    })
  }
}

// Savings Account
let savingsAccount = {
  name: "savings",
  balance: 0,
  allTransactions: [],
  deposit: function (amount) {
    this.balance += amount;
    this.allTransactions.push({
      type: "deposit",
      amount: amount,
    })
  },
  withdraw: function (amount) {
    this.balance -= amount;
    this.allTransactions.push({
      type: "withdrawal",
      amount: amount,
    })
  },
  debit: function (amount, purpose) {
    this.balance -= amount;
    this.allTransactions.push({
      type: "withdrawal",
      amount: amount,
    });
  },
  transfer: function (amount, transferAccount) {
    this.balance -= amount;
    transferAccount.balance += amount;
    transferAccount.allTransactions.push({
      type: "transfer",
      amount: amount,
      purpose: "purpose",
    });
  },
  transfer: function (amount, transferAccount) {
    this.balance -= amount;
    transferAccount.balance += amount;
    transferAccount.allTransactions.push({
      type: "transfer",
      amount: amount,
      purpose: "transfer",
    }),
    this.allTransactions.push({
      type: "transfer",
      amount: amount,
      purpose: "transfer"
    })
  }
}

// This function needs to be called to hide info till we need it
function hideStartingInfo() {
  // Hides savings/checking info and transaction info.
  hideToggle(checking_info);
  hideToggle(savings_info);
  hideToggle(transactions);
}

function printTable(tableId, account, transferMessage) {
  // This will print itmes to table as they are entered
  let newRow = tableId.insertRow(-1);5
  let newCell1 = newRow.insertCell(0);
  let newCell2 = newRow.insertCell(1);
  let newCell3 = newRow.insertCell(2);
  let newCell4 = newRow.insertCell(3);
  newCell1.innerHTML = account.allTransactions[account.allTransactions.length - 1].type;
  newCell3.innerHTML = account.allTransactions[account.allTransactions.length - 1].amount;
  newCell4.innerHTML = account.balance;
  if (account.allTransactions[account.allTransactions.length - 1].purpose != undefined) {
    if(account.allTransactions[account.allTransactions.length - 1].purpose === "transfer") {
    newCell2.innerHTML = transferMessage;
  } else {
    newCell2.innerHTML = account.allTransactions[account.allTransactions.length - 1].purpose;
  } 
  } else {
  newCell2.innerHTML = "";
}
}

// Checks which transaction button is selected and exucutes correct function.
function mainBankChecking() {
  if(transactionType.value === "Debit") {
    runDebitChecking();
    transDescription.value = "";
    transAmount.value = "";
  } else if (transactionType.value === "Deposit") {
    runDepositChecking();
    transAmount.value = "";
  } else if (transactionType.value === "Withdraw") {
    runwithdrawChecking();
    transAmount.value = "";
  } else if (transactionType.value === "Transfer") {
    runTransferChecking();
    transAmount.value = "";
  }
}


    // Checks which transaction button is selected and executes correct function.
    function mainBankSavings() {
      if (transactionTypeSavings.value === "Deposit") {
        runDepositSavings();
        transAmountSavings.value = "";
      } else if (transactionTypeSavings.value === "Withdraw") {
        runWithdrawSavings();
        transAmountSavings.value = "";
      } else if (transactionTypeSavings.value === "Transfer") {
        runTransferSavings();
        transAmountSavings.value = "";
      }
    }

    // Checking Debit
    function runDebitChecking() {
      let howMuch = Number.parseFloat(transAmount.value);
      let forWhat = transDescription.value;
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.");
      } else {
        if (checkingAccount.balance >= howMuch) {
          checkingAccount.debit(howMuch, forWhat);
          displayAccountBalances();
          printTable(table, checkingAccount);
        } else {
          alert("Not enough funds for transaction")
        }
      }
    }

    // Checking Deposit
    function runDepositChecking() {
      let howMuch = Number.parseFloat(transAmount.value);
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.")
      } else {
        checkingAccount.deposit(howMuch);
        displayAccountBalances();
        printTable(table, checkingAccount);
      }
    }

    // Savings Deposit
    function runDepositSavings() {
      let howMuch = Number.parseFloat(transAmountSavings.value);
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.")
      } else {
        savingsAccount.deposit(howMuch);
        displayAccountBalances();
        printTable(tableSavings, savingsAccount);
      }
    }

    // Checking Withdrawal
    function runwithdrawChecking() {
      let howMuch = Number.parseFloat(transAmountAmount.value);
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.");
      } else {
        if (checkingAccount.balance >= howMuch) {
          checkingAccount.withdraw(howMuch);
          displayAccountBalances();
          printTable(table, checkingAccount);
        } else {
          alert("Not enought funds for transaction")
        }
      }
    }

    // Savings Withdrawal
    function runwithdrawSavings() {
      let howMuch = Number.parseFloat(transAmountSavings.value);
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.");
      } else {
        if (savingsAccount.balance >= howMuch) {
          savingsAccount.withdraw(howMuch);
          displayAccountBalances();
          printTable(tableSavings, savingsAccount);
        } else {
          alert("Not enough funds for transaction.")
        }
      }
    }

    // Transfer Checking to Savings
    function runTransferChecking() {
      let howMuch = Number.parseFloat(transAmount.value);
      if (isNaN(howMuch)) {
        alert("Enter positive number.");
      } else {
        if (checkingAccount.balance >= howMuch) {
          checkingAccount.transfer(howMuch, savingsAccount);
          displayAccountBalances();
          printTable(table, checkingAccount, "Transfer to Savings");
          printTable(tableSavings, savingsAccount, "Transfer from Checkings");
        } else {
          alert("Not enough funds for transaction")
        }
      }
    }

    // Transfer Savings to Checking
    function runTransferSavings() {
      let howMuch = Number.parseFloat(transAmountSavings.value);
      if (isNaN(howMuch)) {
        alert("Enter Amount");
      } else if (howMuch <= 0) {
        alert("Enter positive number.");
      } else {
        if (savingsAccount.balance >= howMuch) {
          savingsAccount.transfer(howMuch, checkingAccount);
          displayAccountBalances();
          printTable(tableSavings, savingsAccount, "Transfer to checking");
          printTable(table, checkingAccount, "Transfer from savings");
      
        } else {
          alert("Not enough funds for transaction.")
        }
      }
    }

    // Displays current balance of both accounts
    function displayAccountBalances () {
      document.querySelector("#current_checking_balance").textContent = "Current Balance: $" +  checkingAccount.balance;
      document.querySelector("#current_savings_balance").textContent = "Current Balance: $" +   savingsAccount.balance;
    }

    // Get starting balance of both accounts
    function displayAccountBalances () {
     let checkStart = parseFloat(checkingsStartingBalance.value);
     let saveStart = parseFloat(savingsStartingBalance.value);
     let checkFixed = parseFloat(checkStart.toFixed(2));
     let saveFixed = parseFloat(saveStart.toFixed(2));
     if (isNaN(checkStart) || isNaN(saveStart)) {
      alert("Enter starting balance.")
     } else {
      checkingAccount.balance = checkFixed;
      savingsAccount.balance = saveFixed;
      clearBox("balance_info");
      displayAccountBalances();
      hideToggle(checking_info);
      hideToggle(savings_info);
      hideToggle(transactions);
      hideToggle(balanceInfo);
     }
    }

    // Clears element html
    function clearBox(elementID) {
      document.getElementById(elementID).innerHTML ="";
    }

    // Checks transaction type. If debited it then shows description box. If not it hides it
    function checkTransType() {
      if (transactionType.value === "Debit") {
        desc.getElementsByClassName.display = "block";
        transDescription.value = ""; 
      } else if (transactionType.value === "Deposit") {
        desc.style.display = "none";
      } else if (transactionType.value === "Withdraw") {
        desc.style.display = "none";
      } else if (transactionType.value === "Transfer") {
        desc.style.display = "none";
      }
    }

    // Toggle to hide items
    function hideToggle(itemToHide) {
      if (itemToHide.style.display === "none") {
        itemToHide.style.display = "block";
      } else {
        itemToHide.style.display = "none";
      }
    }

    // Limits input boxes to .00 decimal places. Use this function oninput for input boxes in html
     function validate(event) {
       let x = this.value;
       this.value = (x.indexOf(".") >= 0) ? (x.substr(0, x.indexOf(".")) + x.substr(x.indexOf("."), 3)) : x;
       }
    
      checkingStartingBalance.addEventListener("input", validate);
      savingsStartingBalance.addEventListener("input", validate);
      transAmount.addEventListener("input", validate);
      transAmountSavings.addEventListener("input", validate);
      document.querySelector("#submit_balance").addEventListener("click", getStartingBalance);
      document.querySelector("#submit_transaction").addEventListener("click", () => {
      mainBankChecking();
     });
      document.querySelector("#submit_transaction_savings").addEventListener("click", () => {
      mainBankSavings();
      });
      transactionType.addEventListener("click", checkTransType);

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
  background-color: #414141;
  border-top: none;
}

td:first-child, th:first-child {
  border-left: none;
}

.trans_type {
   background:#e5e5e5;
   border: 1px solid #2b2b2b;
   border-radius: 5px;
   padding: 2px;
   margin: 5px;
}

.submit_trans {
  background: #1c1917;
  color: #e5e5e5;
  border: 1px solid #c4c4c4;
  border-radius: 5px;
  padding: 5px;
  margin: 5px;
  width: 67px;
}

.transaction {
  background: #F5F5F5;
  border: 1px solid #414141;
  border-radius: 5px;
}

</style>
