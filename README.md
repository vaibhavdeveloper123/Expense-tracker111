<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Expense Tracker</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2D3B8E;
            --secondary: #2CB9B0;
            --income: #4CAF50;
            --expense: #F44336;
            --light: #F5F7FA;
            --dark: #333;
            --gray: #888;
            --card-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f0f2f5;
            color: var(--dark);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            margin-bottom: 20px;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: var(--primary);
        }

        .header-controls {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .currency-selector {
            padding: 8px 12px;
            border-radius: 8px;
            border: 1px solid #ddd;
            background-color: white;
            font-size: 14px;
            cursor: pointer;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: var(--secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }

        .balance-card {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: var(--card-shadow);
        }

        .balance-title {
            font-size: 16px;
            margin-bottom: 5px;
            opacity: 0.9;
        }

        .balance-amount {
            font-size: 32px;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .balance-stats {
            display: flex;
            justify-content: space-between;
        }

        .income-stat, .expense-stat {
            text-align: center;
        }

        .income-stat i {
            color: var(--income);
        }

        .expense-stat i {
            color: var(--expense);
        }

        .stat-amount {
            font-weight: bold;
            font-size: 18px;
        }

        .stat-title {
            font-size: 14px;
            opacity: 0.8;
        }

        .quick-actions {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }

        .action-btn {
            background-color: white;
            border: none;
            border-radius: 10px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: var(--card-shadow);
            transition: transform 0.2s;
        }

        .action-btn:hover {
            transform: translateY(-3px);
        }

        .action-btn i {
            font-size: 24px;
            margin-bottom: 8px;
            color: var(--primary);
        }

        .action-btn span {
            font-size: 14px;
            font-weight: 500;
        }

        .section-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .see-all {
            font-size: 14px;
            color: var(--primary);
            cursor: pointer;
        }

        .transactions-list {
            background-color: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: var(--card-shadow);
            margin-bottom: 20px;
        }

        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #eee;
        }

        .transaction-item:last-child {
            border-bottom: none;
        }

        .transaction-left {
            display: flex;
            align-items: center;
        }

        .transaction-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #E3F2FD;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            color: var(--primary);
        }

        .transaction-info h4 {
            font-size: 16px;
            margin-bottom: 3px;
        }

        .transaction-info p {
            font-size: 13px;
            color: var(--gray);
        }

        .transaction-amount {
            font-weight: 600;
        }

        .transaction-actions {
            display: flex;
            gap: 8px;
            margin-left: 10px;
        }

        .delete-btn {
            background: none;
            border: none;
            color: var(--expense);
            cursor: pointer;
            font-size: 14px;
        }

        .income {
            color: var(--income);
        }

        .expense {
            color: var(--expense);
        }

        .budget-card {
            background-color: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: var(--card-shadow);
            margin-bottom: 20px;
        }

        .budget-item {
            margin-bottom: 15px;
        }

        .budget-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }

        .budget-category {
            display: flex;
            align-items: center;
        }

        .budget-category i {
            margin-right: 10px;
            color: var(--primary);
        }

        .budget-amount {
            font-weight: 600;
        }

        .progress-bar {
            height: 8px;
            background-color: #eee;
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            border-radius: 4px;
            background-color: var(--secondary);
        }

        .progress-danger {
            background-color: var(--expense);
        }

        .progress-warning {
            background-color: #FFC107;
        }

        .budget-footer {
            display: flex;
            justify-content: space-between;
            font-size: 12px;
            color: var(--gray);
            margin-top: 3px;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            border-radius: 15px;
            width: 90%;
            max-width: 400px;
            padding: 20px;
            animation: modalFadeIn 0.3s;
        }

        @keyframes modalFadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 20px;
            font-weight: 600;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: var(--gray);
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }

        .type-toggle {
            display: flex;
            border: 1px solid #ddd;
            border-radius: 8px;
            overflow: hidden;
            margin-bottom: 15px;
        }

        .type-toggle button {
            flex: 1;
            padding: 12px;
            border: none;
            background: none;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
        }

        .type-toggle button.active {
            background-color: var(--primary);
            color: white;
        }

        .btn {
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-weight: 500;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: #1E2B7B;
        }

        .tabs {
            display: flex;
            border-bottom: 1px solid #ddd;
            margin-bottom: 20px;
        }

        .tab {
            padding: 10px 20px;
            cursor: pointer;
            position: relative;
        }

        .tab.active {
            color: var(--primary);
            font-weight: 500;
        }

        .tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 3px;
            background-color: var(--primary);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .chart-container {
            height: 200px;
            margin-bottom: 20px;
        }

        .confirmation-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1001;
            justify-content: center;
            align-items: center;
        }

        .confirmation-content {
            background-color: white;
            border-radius: 15px;
            width: 90%;
            max-width: 400px;
            padding: 20px;
            text-align: center;
        }

        .confirmation-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }

        .confirmation-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-weight: 500;
            cursor: pointer;
        }

        .confirm-btn {
            background-color: var(--expense);
            color: white;
        }

        .cancel-btn {
            background-color: #eee;
            color: var(--dark);
        }

        .grocery-list {
            background-color: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: var(--card-shadow);
            margin-bottom: 20px;
        }

        .grocery-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }

        .grocery-item:last-child {
            border-bottom: none;
        }

        .grocery-item input[type="checkbox"] {
            margin-right: 10px;
        }

        .grocery-item .item-name {
            flex-grow: 1;
        }

        .grocery-item .item-quantity {
            margin-right: 15px;
            color: var(--gray);
        }

        .calculator-container {
            background-color: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: var(--card-shadow);
            margin-bottom: 20px;
        }

        .calculator-tabs {
            display: flex;
            border-bottom: 1px solid #ddd;
            margin-bottom: 15px;
        }

        .calculator-tab {
            padding: 8px 15px;
            cursor: pointer;
            position: relative;
        }

        .calculator-tab.active {
            color: var(--primary);
            font-weight: 500;
        }

        .calculator-tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 3px;
            background-color: var(--primary);
        }

        .calculator-content {
            display: none;
        }

        .calculator-content.active {
            display: block;
        }

        .calculator-result {
            margin-top: 15px;
            padding: 10px;
            background-color: #f5f7fa;
            border-radius: 8px;
            font-weight: 600;
        }

        @media (max-width: 768px) {
            .quick-actions {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        @media (max-width: 480px) {
            .quick-actions {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .balance-stats {
                flex-direction: column;
                gap: 15px;
            }
            
            .stat-amount {
                font-size: 16px;
            }
            
            .header-controls {
                gap: 10px;
            }
            
            .currency-selector {
                padding: 6px 8px;
                font-size: 12px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">💰 ExpenseTracker</div>
            <div class="header-controls">
                <select class="currency-selector" id="currency-selector">
                    <option value="USD">USD ($)</option>
                    <option value="EUR">EUR (€)</option>
                    <option value="GBP">GBP (£)</option>
                    <option value="JPY">JPY (¥)</option>
                    <option value="CAD">CAD ($)</option>
                    <option value="AUD">AUD ($)</option>
                    <option value="INR">INR (₹)</option>
                    <option value="CNY">CNY (¥)</option>
                </select>
                <div class="user-avatar">👤</div>
            </div>
        </header>

        <div class="balance-card">
            <div class="balance-title">Total Balance</div>
            <div class="balance-amount" id="total-balance">$0.00</div>
            <div class="balance-stats">
                <div class="income-stat">
                    <i class="fas fa-arrow-up"></i>
                    <div class="stat-amount" id="total-income">$0.00</div>
                    <div class="stat-title">Income 💰</div>
                </div>
                <div class="expense-stat">
                    <i class="fas fa-arrow-down"></i>
                    <div class="stat-amount" id="total-expense">$0.00</div>
                    <div class="stat-title">Expenses 💸</div>
                </div>
            </div>
        </div>

        <div class="quick-actions">
            <div class="action-btn" id="add-expense">
                <i class="fas fa-minus-circle"></i>
                <span>Add Expense ➖</span>
            </div>
            <div class="action-btn" id="add-income">
                <i class="fas fa-plus-circle"></i>
                <span>Add Income ➕</span>
            </div>
            <div class="action-btn" id="set-budget">
                <i class="fas fa-wallet"></i>
                <span>Set Budget 💰</span>
            </div>
            <div class="action-btn" id="view-calculators">
                <i class="fas fa-calculator"></i>
                <span>Calculators 🧮</span>
            </div>
            <div class="action-btn" id="view-grocery">
                <i class="fas fa-shopping-basket"></i>
                <span>Grocery List 🛒</span>
            </div>
        </div>

        <div class="tabs">
            <div class="tab active" data-tab="transactions">💳 Transactions</div>
            <div class="tab" data-tab="budgets">📊 Budgets</div>
            <div class="tab" data-tab="analytics">📈 Analytics</div>
            <div class="tab" data-tab="calculators" style="display: none;">🧮 Calculators</div>
            <div class="tab" data-tab="grocery" style="display: none;">🛒 Grocery List</div>
        </div>

        <div class="tab-content active" id="transactions">
            <div class="section-title">
                Recent Transactions
                <span class="see-all">See All 👉</span>
            </div>
            <div class="transactions-list" id="transactions-container">
                <div class="no-transactions">📭 No transactions yet. Add your first transaction!</div>
            </div>
        </div>

        <div class="tab-content" id="budgets">
            <div class="section-title">
                Monthly Budgets
                <span class="see-all">See All 👉</span>
            </div>
            <div class="budget-card" id="budgets-container">
                <div class="no-budgets">📭 No budgets set up yet. Create your first budget!</div>
            </div>
        </div>

        <div class="tab-content" id="analytics">
            <div class="section-title">
                Spending Analytics
            </div>
            <div class="chart-container">
                <canvas id="spendingChart"></canvas>
            </div>
            <div class="section-title">
                Category Breakdown
            </div>
            <div class="chart-container">
                <canvas id="categoryChart"></canvas>
            </div>
        </div>

        <div class="tab-content" id="calculators">
            <div class="section-title">
                Financial Calculators 🧮
            </div>
            <div class="calculator-container">
                <div class="calculator-tabs">
                    <div class="calculator-tab active" data-calculator="emi">🏦 EMI</div>
                    <div class="calculator-tab" data-calculator="percentage">% Percentage</div>
                    <div class="calculator-tab" data-calculator="interest">💵 Interest</div>
                </div>

                <div class="calculator-content active" id="emi-calculator">
                    <div class="form-group">
                        <label for="loan-amount">💰 Loan Amount</label>
                        <input type="number" id="loan-amount" class="form-control" placeholder="e.g. 100000">
                    </div>
                    <div class="form-group">
                        <label for="interest-rate">📈 Interest Rate (% p.a.)</label>
                        <input type="number" id="interest-rate" class="form-control" placeholder="e.g. 8.5">
                    </div>
                    <div class="form-group">
                        <label for="loan-tenure">⏳ Loan Tenure (months)</label>
                        <input type="number" id="loan-tenure" class="form-control" placeholder="e.g. 60">
                    </div>
                    <button class="btn btn-primary" id="calculate-emi">🧮 Calculate EMI</button>
                    <div class="calculator-result" id="emi-result"></div>
                </div>

                <div class="calculator-content" id="percentage-calculator">
                    <div class="form-group">
                        <label for="percentage-value">🔢 Value</label>
                        <input type="number" id="percentage-value" class="form-control" placeholder="e.g. 100">
                    </div>
                    <div class="form-group">
                        <label for="percentage">% Percentage</label>
                        <input type="number" id="percentage" class="form-control" placeholder="e.g. 15">
                    </div>
                    <button class="btn btn-primary" id="calculate-percentage">🧮 Calculate</button>
                    <div class="calculator-result" id="percentage-result"></div>
                </div>

                <div class="calculator-content" id="interest-calculator">
                    <div class="form-group">
                        <label for="principal-amount">💰 Principal Amount</label>
                        <input type="number" id="principal-amount" class="form-control" placeholder="e.g. 10000">
                    </div>
                    <div class="form-group">
                        <label for="interest-rate-simple">📈 Interest Rate (% p.a.)</label>
                        <input type="number" id="interest-rate-simple" class="form-control" placeholder="e.g. 5">
                    </div>
                    <div class="form-group">
                        <label for="time-period">⏳ Time Period (years)</label>
                        <input type="number" id="time-period" class="form-control" placeholder="e.g. 3">
                    </div>
                    <button class="btn btn-primary" id="calculate-interest">🧮 Calculate Interest</button>
                    <div class="calculator-result" id="interest-result"></div>
                </div>
            </div>
        </div>

        <div class="tab-content" id="grocery">
            <div class="section-title">
                🛒 Grocery List
                <button class="btn btn-primary" id="add-grocery-item" style="width: auto; padding: 8px 15px;">
                    <i class="fas fa-plus"></i> Add Item
                </button>
            </div>
            <div class="grocery-list" id="grocery-container">
                <div class="no-items">🛍️ Your grocery list is empty. Add some items!</div>
            </div>
        </div>
    </div>

    <!-- Add Transaction Modal -->
    <div class="modal" id="transaction-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">💸 Add Transaction</div>
                <button class="close-modal">&times;</button>
            </div>
            <form id="transaction-form">
                <div class="type-toggle">
                    <button type="button" class="active" data-type="expense">Expense ➖</button>
                    <button type="button" data-type="income">Income ➕</button>
                </div>
                <div class="form-group">
                    <label for="amount">💰 Amount</label>
                    <input type="number" id="amount" class="form-control" placeholder="0.00" step="0.01" required>
                </div>
                <div class="form-group">
                    <label for="category">🏷️ Category</label>
                    <select id="category" class="form-control" required>
                        <option value="">Select Category</option>
                        <option value="food">🍔 Food</option>
                        <option value="transport">🚗 Transport</option>
                        <option value="shopping">🛍️ Shopping</option>
                        <option value="housing">🏠 Housing</option>
                        <option value="entertainment">🎬 Entertainment</option>
                        <option value="salary">💼 Salary</option>
                        <option value="other">✨ Other</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="date">📅 Date</label>
                    <input type="date" id="date" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="description">📝 Description (Optional)</label>
                    <input type="text" id="description" class="form-control" placeholder="Add a note">
                </div>
                <button type="submit" class="btn btn-primary">💾 Save Transaction</button>
            </form>
        </div>
    </div>

    <!-- Set Budget Modal -->
    <div class="modal" id="budget-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">💰 Set Budget</div>
                <button class="close-modal">&times;</button>
            </div>
            <form id="budget-form">
                <div class="form-group">
                    <label for="budget-category">🏷️ Category</label>
                    <select id="budget-category" class="form-control" required>
                        <option value="">Select Category</option>
                        <option value="food">🍔 Food</option>
                        <option value="transport">🚗 Transport</option>
                        <option value="shopping">🛍️ Shopping</option>
                        <option value="housing">🏠 Housing</option>
                        <option value="entertainment">🎬 Entertainment</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="budget-amount">💰 Budget Amount</label>
                    <input type="number" id="budget-amount" class="form-control" placeholder="0.00" step="0.01" required>
                </div>
                <button type="submit" class="btn btn-primary">💾 Save Budget</button>
            </form>
        </div>
    </div>

    <!-- Add Grocery Item Modal -->
    <div class="modal" id="grocery-modal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">🛒 Add Grocery Item</div>
                <button class="close-modal">&times;</button>
            </div>
            <form id="grocery-form">
                <div class="form-group">
                    <label for="grocery-name">📝 Item Name</label>
                    <input type="text" id="grocery-name" class="form-control" placeholder="e.g. Milk" required>
                </div>
                <div class="form-group">
                    <label for="grocery-quantity">🔢 Quantity</label>
                    <input type="text" id="grocery-quantity" class="form-control" placeholder="e.g. 1 liter">
                </div>
                <button type="submit" class="btn btn-primary">💾 Add Item</button>
            </form>
        </div>
    </div>

    <!-- Delete Confirmation Modal -->
    <div class="confirmation-modal" id="confirmation-modal">
        <div class="confirmation-content">
            <h3>🗑️ Delete Transaction</h3>
            <p>Are you sure you want to delete this transaction?</p>
            <div class="confirmation-buttons">
                <button class="confirmation-btn cancel-btn" id="cancel-delete">❌ Cancel</button>
                <button class="confirmation-btn confirm-btn" id="confirm-delete">✅ Delete</button>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Data structure
        let transactions = [];
        let budgets = [];
        let groceryList = [];
        let currentCurrency = 'USD'; // Default currency

        // Currency symbols and formatting
        const currencySymbols = {
            USD: '$',
            EUR: '€',
            GBP: '£',
            JPY: '¥',
            CAD: '$',
            AUD: '$',
            INR: '₹',
            CNY: '¥'
        };

        // DOM Elements
        const transactionsContainer = document.getElementById('transactions-container');
        const budgetsContainer = document.getElementById('budgets-container');
        const groceryContainer = document.getElementById('grocery-container');
        const transactionModal = document.getElementById('transaction-modal');
        const budgetModal = document.getElementById('budget-modal');
        const groceryModal = document.getElementById('grocery-modal');
        const transactionForm = document.getElementById('transaction-form');
        const budgetForm = document.getElementById('budget-form');
        const groceryForm = document.getElementById('grocery-form');
        const typeToggleButtons = document.querySelectorAll('.type-toggle button');
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        const calculatorTabs = document.querySelectorAll('.calculator-tab');
        const calculatorContents = document.querySelectorAll('.calculator-content');
        const addExpenseBtn = document.getElementById('add-expense');
        const addIncomeBtn = document.getElementById('add-income');
        const setBudgetBtn = document.getElementById('set-budget');
        const viewCalculatorsBtn = document.getElementById('view-calculators');
        const viewGroceryBtn = document.getElementById('view-grocery');
        const addGroceryBtn = document.getElementById('add-grocery-item');
        const seeAllButtons = document.querySelectorAll('.see-all');
        const totalBalanceEl = document.getElementById('total-balance');
        const totalIncomeEl = document.getElementById('total-income');
        const totalExpenseEl = document.getElementById('total-expense');
        const confirmationModal = document.getElementById('confirmation-modal');
        const cancelDeleteBtn = document.getElementById('cancel-delete');
        const confirmDeleteBtn = document.getElementById('confirm-delete');
        const calculateEmiBtn = document.getElementById('calculate-emi');
        const calculatePercentageBtn = document.getElementById('calculate-percentage');
        const calculateInterestBtn = document.getElementById('calculate-interest');
        const currencySelector = document.getElementById('currency-selector');
        let spendingChart, categoryChart;
        let transactionToDelete = null;

        // Helper functions for localStorage
        function saveDataToLocalStorage() {
            localStorage.setItem('expenseTracker_transactions', JSON.stringify(transactions));
            localStorage.setItem('expenseTracker_budgets', JSON.stringify(budgets));
            localStorage.setItem('expenseTracker_grocery', JSON.stringify(groceryList));
            localStorage.setItem('expenseTracker_currency', currentCurrency);
        }

        function loadDataFromLocalStorage() {
            const savedTransactions = localStorage.getItem('expenseTracker_transactions');
            const savedBudgets = localStorage.getItem('expenseTracker_budgets');
            const savedGrocery = localStorage.getItem('expenseTracker_grocery');
            const savedCurrency = localStorage.getItem('expenseTracker_currency');
            
            if (savedTransactions) {
                transactions = JSON.parse(savedTransactions);
            }
            
            if (savedBudgets) {
                budgets = JSON.parse(savedBudgets);
            }

            if (savedGrocery) {
                groceryList = JSON.parse(savedGrocery);
            }

            if (savedCurrency) {
                currentCurrency = savedCurrency;
                currencySelector.value = currentCurrency;
            }
        }

        // Format currency based on current selection
        function formatCurrency(amount) {
            const symbol = currencySymbols[currentCurrency] || '$';
            return `${symbol}${amount.toFixed(2)}`;
        }

        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            loadDataFromLocalStorage();
            updateBalance();
            renderTransactions();
            renderBudgets();
            renderGroceryList();
            initCharts();
            
            // Set today's date as default in the form
            document.getElementById('date').valueAsDate = new Date();
        });

        // Event Listeners
        addExpenseBtn.addEventListener('click', () => openTransactionModal('expense'));
        addIncomeBtn.addEventListener('click', () => openTransactionModal('income'));
        setBudgetBtn.addEventListener('click', () => openBudgetModal());
        viewCalculatorsBtn.addEventListener('click', () => showTab('calculators'));
        viewGroceryBtn.addEventListener('click', () => showTab('grocery'));
        addGroceryBtn.addEventListener('click', () => openGroceryModal());

        currencySelector.addEventListener('change', function() {
            currentCurrency = this.value;
            saveDataToLocalStorage();
            updateBalance();
            renderTransactions();
            renderBudgets();
        });

        typeToggleButtons.forEach(button => {
            button.addEventListener('click', function() {
                typeToggleButtons.forEach(btn => btn.classList.remove('active'));
                this.classList.add('active');
            });
        });

        tabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const tabId = this.getAttribute('data-tab');
                showTab(tabId);
            });
        });

        calculatorTabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const calculatorId = this.getAttribute('data-calculator');
                
                calculatorTabs.forEach(t => t.classList.remove('active'));
                calculatorContents.forEach(c => c.classList.remove('active'));
                
                this.classList.add('active');
                document.getElementById(`${calculatorId}-calculator`).classList.add('active');
            });
        });

        seeAllButtons.forEach(button => {
            button.addEventListener('click', function() {
                alert('This would show all transactions/budgets in a separate view');
            });
        });

        transactionForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const type = document.querySelector('.type-toggle button.active').getAttribute('data-type');
            const amount = parseFloat(document.getElementById('amount').value);
            const category = document.getElementById('category').value;
            const date = document.getElementById('date').value;
            const description = document.getElementById('description').value;
            
            if (!amount || !category || !date) {
                alert('Please fill in all required fields');
                return;
            }
            
            const newTransaction = {
                id: Date.now(),
                type,
                amount,
                category,
                date,
                description: description || `${category} ${type}`
            };
            
            transactions.unshift(newTransaction);
            updateBalance();
            
            saveDataToLocalStorage();
            renderTransactions();
            updateCharts();
            
            closeTransactionModal();
            transactionForm.reset();
            document.getElementById('date').valueAsDate = new Date();
        });

        budgetForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const category = document.getElementById('budget-category').value;
            const amount = parseFloat(document.getElementById('budget-amount').value);
            
            if (!category || !amount) {
                alert('Please fill in all fields');
                return;
            }
            
            // Update or add budget
            const existingBudgetIndex = budgets.findIndex(b => b.category === category);
            if (existingBudgetIndex >= 0) {
                budgets[existingBudgetIndex].budget = amount;
            } else {
                budgets.push({
                    category,
                    budget: amount,
                    spent: 0
                });
            }
            
            saveDataToLocalStorage();
            renderBudgets();
            closeBudgetModal();
            budgetForm.reset();
        });

        groceryForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const name = document.getElementById('grocery-name').value;
            const quantity = document.getElementById('grocery-quantity').value;
            
            if (!name) {
                alert('Please enter an item name');
                return;
            }
            
            const newItem = {
                id: Date.now(),
                name,
                quantity: quantity || '1',
                completed: false
            };
            
            groceryList.unshift(newItem);
            saveDataToLocalStorage();
            renderGroceryList();
            
            closeGroceryModal();
            groceryForm.reset();
        });

        document.querySelectorAll('.close-modal').forEach(btn => {
            btn.addEventListener('click', function() {
                const modal = this.closest('.modal');
                modal.style.display = 'none';
            });
        });

        document.querySelectorAll('.modal').forEach(modal => {
            modal.addEventListener('click', function(e) {
                if (e.target === this) {
                    this.style.display = 'none';
                }
            });
        });

        cancelDeleteBtn.addEventListener('click', closeConfirmationModal);
        confirmDeleteBtn.addEventListener('click', function() {
            if (transactionToDelete) {
                deleteTransaction(transactionToDelete);
                closeConfirmationModal();
            }
        });

        calculateEmiBtn.addEventListener('click', calculateEMI);
        calculatePercentageBtn.addEventListener('click', calculatePercentage);
        calculateInterestBtn.addEventListener('click', calculateInterest);

        // Functions
        function showTab(tabId) {
            tabs.forEach(t => t.classList.remove('active'));
            tabContents.forEach(c => c.classList.remove('active'));
            
            document.querySelector(`.tab[data-tab="${tabId}"]`).classList.add('active');
            document.getElementById(tabId).classList.add('active');
        }

        function openTransactionModal(type) {
            transactionModal.style.display = 'flex';
            typeToggleButtons.forEach(button => {
                button.classList.remove('active');
                if (button.getAttribute('data-type') === type) {
                    button.classList.add('active');
                }
            });
            
            setTimeout(() => {
                document.getElementById('amount').focus();
            }, 100);
        }

        function openBudgetModal() {
            budgetModal.style.display = 'flex';
            setTimeout(() => {
                document.getElementById('budget-category').focus();
            }, 100);
        }

        function openGroceryModal() {
            groceryModal.style.display = 'flex';
            setTimeout(() => {
                document.getElementById('grocery-name').focus();
            }, 100);
        }

        function openConfirmationModal(transactionId) {
            transactionToDelete = transactionId;
            confirmationModal.style.display = 'flex';
        }

        function closeTransactionModal() {
            transactionModal.style.display = 'none';
        }

        function closeBudgetModal() {
            budgetModal.style.display = 'none';
        }

        function closeGroceryModal() {
            groceryModal.style.display = 'none';
        }

        function closeConfirmationModal() {
            transactionToDelete = null;
            confirmationModal.style.display = 'none';
        }

        function deleteTransaction(transactionId) {
            transactions = transactions.filter(t => t.id !== transactionId);
            saveDataToLocalStorage();
            updateBalance();
            renderTransactions();
            updateCharts();
        }

        function toggleGroceryItem(itemId) {
            const item = groceryList.find(item => item.id === itemId);
            if (item) {
                item.completed = !item.completed;
                saveDataToLocalStorage();
                renderGroceryList();
            }
        }

        function removeGroceryItem(itemId) {
            groceryList = groceryList.filter(item => item.id !== itemId);
            saveDataToLocalStorage();
            renderGroceryList();
        }

        function updateBalance() {
            const income = transactions
                .filter(t => t.type === 'income')
                .reduce((sum, t) => sum + t.amount, 0);
            
            const expenses = transactions
                .filter(t => t.type === 'expense')
                .reduce((sum, t) => sum + t.amount, 0);
            
            const balance = income - expenses;
            
            totalBalanceEl.textContent = formatCurrency(balance);
            totalIncomeEl.textContent = formatCurrency(income);
            totalExpenseEl.textContent = formatCurrency(expenses);
        }

        function renderTransactions() {
            transactionsContainer.innerHTML = '';
            
            if (transactions.length === 0) {
                transactionsContainer.innerHTML = '<div class="no-transactions">📭 No transactions yet. Add your first transaction!</div>';
                return;
            }
            
            const sortedTransactions = [...transactions].sort((a, b) => new Date(b.date) - new Date(a.date));
            
            sortedTransactions.slice(0, 5).forEach(transaction => {
                const transactionEl = document.createElement('div');
                transactionEl.className = 'transaction-item';
                
                const categoryIcon = getCategoryIcon(transaction.category);
                const formattedDate = formatDate(transaction.date);
                const amountClass = transaction.type === 'income' ? 'income' : 'expense';
                
                transactionEl.innerHTML = `
                    <div class="transaction-left">
                        <div class="transaction-icon">
                            ${getCategoryEmoji(transaction.category)}
                        </div>
                        <div class="transaction-info">
                            <h4>${transaction.description}</h4>
                            <p>${formattedDate}</p>
                        </div>
                    </div>
                    <div class="transaction-amount ${amountClass}">
                        ${transaction.type === 'expense' ? '-' : '+'}${formatCurrency(transaction.amount)}
                        <button class="delete-btn" data-id="${transaction.id}">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                
                transactionsContainer.appendChild(transactionEl);
            });

            document.querySelectorAll('.delete-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const transactionId = parseInt(this.getAttribute('data-id'));
                    openConfirmationModal(transactionId);
                });
            });
        }

        function renderBudgets() {
            budgetsContainer.innerHTML = '';
            
            if (budgets.length === 0) {
                budgetsContainer.innerHTML = '<div class="no-budgets">📭 No budgets set up yet. Create your first budget!</div>';
                return;
            }
            
            budgets.forEach(budget => {
                const budgetEl = document.createElement('div');
                budgetEl.className = 'budget-item';
                
                budgetEl.innerHTML = `
                    <div class="budget-header">
                        <div class="budget-category">
                            <span>${getCategoryEmoji(budget.category)}</span>
                            ${capitalizeFirstLetter(budget.category)}
                        </div>
                        <div class="budget-amount">
                            ${formatCurrency(budget.budget)}
                        </div>
                    </div>
                `;
                
                budgetsContainer.appendChild(budgetEl);
            });
        }

        function renderGroceryList() {
            groceryContainer.innerHTML = '';
            
            if (groceryList.length === 0) {
                groceryContainer.innerHTML = '<div class="no-items">🛍️ Your grocery list is empty. Add some items!</div>';
                return;
            }
            
            groceryList.forEach(item => {
                const itemEl = document.createElement('div');
                itemEl.className = 'grocery-item';
                
                itemEl.innerHTML = `
                    <div>
                        <input type="checkbox" id="item-${item.id}" ${item.completed ? 'checked' : ''}>
                        <span class="item-name" style="${item.completed ? 'text-decoration: line-through; color: var(--gray);' : ''}">
                            ${item.name}
                        </span>
                    </div>
                    <div>
                        <span class="item-quantity">${item.quantity}</span>
                        <button class="delete-btn" data-id="${item.id}">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                
                groceryContainer.appendChild(itemEl);
                
                // Add event listeners
                document.getElementById(`item-${item.id}`).addEventListener('change', () => toggleGroceryItem(item.id));
                itemEl.querySelector('.delete-btn').addEventListener('click', (e) => {
                    e.stopPropagation();
                    removeGroceryItem(item.id);
                });
            });
        }

        function calculateEMI() {
            const principal = parseFloat(document.getElementById('loan-amount').value);
            const rate = parseFloat(document.getElementById('interest-rate').value) / 100 / 12;
            const months = parseFloat(document.getElementById('loan-tenure').value);
            
            if (!principal || !rate || !months) {
                alert('Please fill in all fields');
                return;
            }
            
            const emi = principal * rate * Math.pow(1 + rate, months) / (Math.pow(1 + rate, months) - 1);
            const totalPayment = emi * months;
            const totalInterest = totalPayment - principal;
            
            document.getElementById('emi-result').innerHTML = `
                <p>📅 Monthly EMI: <strong>${formatCurrency(emi)}</strong></p>
                <p>💰 Total Payment: <strong>${formatCurrency(totalPayment)}</strong></p>
                <p>💸 Total Interest: <strong>${formatCurrency(totalInterest)}</strong></p>
            `;
        }

        function calculatePercentage() {
            const value = parseFloat(document.getElementById('percentage-value').value);
            const percentage = parseFloat(document.getElementById('percentage').value);
            
            if (!value || !percentage) {
                alert('Please fill in all fields');
                return;
            }
            
            const result = (value * percentage) / 100;
            
            document.getElementById('percentage-result').innerHTML = `
                <p>${percentage}% of ${formatCurrency(value)} = <strong>${formatCurrency(result)}</strong></p>
                <p>📊 ${percentage}% of ${formatCurrency(value)} is <strong>${formatCurrency(result)}</strong></p>
            `;
        }

        function calculateInterest() {
            const principal = parseFloat(document.getElementById('principal-amount').value);
            const rate = parseFloat(document.getElementById('interest-rate-simple').value) / 100;
            const years = parseFloat(document.getElementById('time-period').value);
            
            if (!principal || !rate || !years) {
                alert('Please fill in all fields');
                return;
            }
            
            const interest = principal * rate * years;
            const total = principal + interest;
            
            document.getElementById('interest-result').innerHTML = `
                <p>💵 Simple Interest: <strong>${formatCurrency(interest)}</strong></p>
                <p>💰 Total Amount: <strong>${formatCurrency(total)}</strong></p>
                <p>📅 Over ${years} year${years > 1 ? 's' : ''}</p>
            `;
        }

        function initCharts() {
            const spendingCtx = document.getElementById('spendingChart').getContext('2d');
            spendingChart = new Chart(spendingCtx, {
                type: 'line',
                data: {
                    labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
                    datasets: [{
                        label: 'Weekly Spending',
                        data: [0, 0, 0, 0, 0, 0, 0],
                        borderColor: 'rgba(44, 185, 176, 1)',
                        backgroundColor: 'rgba(44, 185, 176, 0.2)',
                        tension: 0.4,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        }
                    }
                }
            });

            const categoryCtx = document.getElementById('categoryChart').getContext('2d');
            categoryChart = new Chart(categoryCtx, {
                type: 'doughnut',
                data: {
                    labels: ['No data'],
                    datasets: [{
                        data: [1],
                        backgroundColor: ['rgba(200, 200, 200, 0.7)'],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        }
                    }
                }
            });
        }

        function updateCharts() {
            // This would update charts with real data in a full implementation
        }

        function getCategoryIcon(category) {
            const icons = {
                food: 'fa-utensils',
                transport: 'fa-car',
                shopping: 'fa-shopping-bag',
                housing: 'fa-home',
                entertainment: 'fa-film',
                salary: 'fa-money-bill-wave',
                other: 'fa-ellipsis-h'
            };
            return icons[category] || 'fa-ellipsis-h';
        }

        function getCategoryEmoji(category) {
            const emojis = {
                food: '🍔',
                transport: '🚗',
                shopping: '🛍️',
                housing: '🏠',
                entertainment: '🎬',
                salary: '💰',
                other: '✨'
            };
            return emojis[category] || '✨';
        }

        function formatDate(dateString, short = false) {
            if (!dateString) return '';
            
            const date = new Date(dateString);
            const today = new Date();
            const yesterday = new Date(today);
            yesterday.setDate(yesterday.getDate() - 1);
            
            if (date.toDateString() === today.toDateString()) {
                return 'Today';
            } else if (date.toDateString() === yesterday.toDateString()) {
                return 'Yesterday';
            } else if (short) {
                return date.toLocaleDateString('en-US', { month: 'short', day: 'numeric' });
            } else {
                return date.toLocaleDateString('en-US', { month: 'long', day: 'numeric' });
            }
        }

        function capitalizeFirstLetter(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        }
    </script>
</body>
</html>
