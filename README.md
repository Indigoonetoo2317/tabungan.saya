<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Tabungan</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            padding: 30px;
            background: linear-gradient(135deg, #4CAF50 0%, #45a049 100%);
            color: white;
        }

        .editable-section {
            margin-bottom: 20px;
        }

        .editable-display {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            padding: 5px;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        .editable-display:hover {
            background-color: rgba(255, 255, 255, 0.1);
        }

        .editable-input {
            display: none;
            gap: 10px;
            align-items: center;
        }

        .editable-input input {
            padding: 8px 12px;
            border: 2px solid white;
            border-radius: 5px;
            font-size: inherit;
            background: white;
            color: #333;
        }

        .edit-btn, .save-btn, .cancel-btn {
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: 5px 8px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 12px;
            transition: all 0.3s ease;
        }

        .edit-btn:hover, .save-btn:hover, .cancel-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .name-text {
            font-size: 28px;
            font-weight: bold;
        }

        .goal-text {
            font-size: 18px;
            opacity: 0.9;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .current-amount {
            background: rgba(255, 255, 255, 0.15);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            text-align: center;
        }

        .amount-label {
            font-size: 16px;
            opacity: 0.9;
            margin-bottom: 5px;
        }

        .amount-value {
            font-size: 36px;
            font-weight: bold;
        }

        .main-content {
            padding: 30px;
        }

        .divider {
            height: 2px;
            background: linear-gradient(90deg, #4CAF50, #81C784);
            margin: 30px 0;
            border-radius: 1px;
        }

        .input-section {
            display: flex;
            gap: 15px;
            margin-bottom: 30px;
            align-items: center;
        }

        .input-field {
            flex: 1;
            padding: 15px 20px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 18px;
            transition: border-color 0.3s ease;
        }

        .input-field:focus {
            outline: none;
            border-color: #4CAF50;
            box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.1);
        }

        .add-btn {
            padding: 15px 30px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
        }

        .add-btn:hover {
            background: #45a049;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.3);
        }

        .error-message {
            color: #f44336;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }

        .history-section h3 {
            color: #333;
            margin-bottom: 20px;
            font-size: 22px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .history-header {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .reset-btn {
            padding: 8px 15px;
            background: #f44336;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .reset-btn:hover {
            background: #d32f2f;
            transform: translateY(-1px);
        }

        .history-list {
            max-height: 400px;
            overflow-y: auto;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            background: #f8f9fa;
            margin-bottom: 10px;
            border-radius: 10px;
            border-left: 4px solid #4CAF50;
            transition: all 0.3s ease;
            position: relative;
        }

        .history-item:hover {
            background: #e8f5e8;
            transform: translateX(5px);
        }

        .history-date {
            color: #666;
            font-size: 14px;
        }

        .history-amount {
            color: #4CAF50;
            font-weight: 600;
            font-size: 18px;
        }

        .delete-btn {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            background: #f44336;
            color: white;
            border: none;
            border-radius: 3px;
            padding: 5px 8px;
            font-size: 12px;
            cursor: pointer;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .history-item:hover .delete-btn {
            opacity: 1;
        }

        .delete-btn:hover {
            background: #d32f2f;
        }

        .no-history {
            text-align: center;
            color: #999;
            font-style: italic;
            padding: 40px;
        }

        /* Calculator */
        .calculator-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 12px; /* Ubah dari 50% menjadi 12px untuk bentuk kotak */
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
            z-index: 100;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .calculator-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }

        .calculator-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .calculator {
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            max-width: 350px;
            width: 90%;
            position: relative;
            border: 2px solid #e0e0e0; /* Tambahkan border */
        }

        .calculator-header {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
            font-size: 20px;
            font-weight: 600;
            padding: 10px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-radius: 10px;
            margin: -10px -10px 20px -10px;
        }

        .calculator-display {
            width: 100%;
            height: 70px;
            background: #f8f9fa;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 24px;
            text-align: right;
            padding: 0 15px;
            margin-bottom: 15px;
            font-weight: 600;
            color: #333;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .calculator-buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            padding: 10px;
            background: #f8f9fa;
            border-radius: 15px;
            border: 1px solid #e0e0e0;
        }

        .calc-btn {
            height: 55px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .calc-btn.number {
            background: #f8f9fa;
            color: #333;
        }

        .calc-btn.operator {
            background: #667eea;
            color: white;
        }

        .calc-btn.equals {
            background: #4CAF50;
            color: white;
        }

        .calc-btn.clear {
            background: #f44336;
            color: white;
        }

        .calc-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }

        .calc-btn:active {
            transform: scale(0.95);
        }

        .close-calculator {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 24px;
            color: #999;
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .close-calculator:hover {
            color: #333;
        }

        .use-result-btn {
            width: 100%;
            margin-top: 15px;
            padding: 12px;
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .use-result-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.3);
        }

        .use-result-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        /* Icons */
        .icon {
            width: 20px;
            height: 20px;
            display: inline-block;
            vertical-align: middle;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            
            .header {
                padding: 20px;
            }
            
            .main-content {
                padding: 20px;
            }
            
            .input-section {
                flex-direction: column;
                gap: 10px;
            }
            
            .add-btn {
                width: 100%;
            }
            
            .calculator-btn {
                top: 10px;
                right: 10px;
                width: 55px;
                height: 55px;
                font-size: 20px;
                border-radius: 10px;
            }
            
            .calculator {
                margin: 10px;
                padding: 20px;
                max-width: calc(100% - 20px);
            }
            
            .calculator-buttons {
                gap: 8px;
                padding: 8px;
            }
            
            .calc-btn {
                height: 50px;
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header Section -->
        <div class="header">
            <!-- Editable Name -->
            <div class="editable-section">
                <div class="editable-display" id="nameDisplay" onclick="editName()">
                    <span class="name-text" id="nameText">Nama Anda</span>
                    <button class="edit-btn">✏️ Edit</button>
                </div>
                <div class="editable-input" id="nameInput">
                    <input type="text" id="nameField" class="name-text" placeholder="Masukkan nama Anda">
                    <button class="save-btn" onclick="saveName()">✓ Simpan</button>
                    <button class="cancel-btn" onclick="cancelEditName()">✗ Batal</button>
                </div>
            </div>

            <!-- Editable Goal -->
            <div class="editable-section">
                <div class="editable-display" id="goalDisplay" onclick="editGoal()">
                    <span class="goal-text" id="goalText">🎯 Tujuan Menabung</span>
                    <button class="edit-btn">✏️ Edit</button>
                </div>
                <div class="editable-input" id="goalInput">
                    <input type="text" id="goalField" class="goal-text" placeholder="Masukkan tujuan menabung">
                    <button class="save-btn" onclick="saveGoal()">✓ Simpan</button>
                    <button class="cancel-btn" onclick="cancelEditGoal()">✗ Batal</button>
                </div>
            </div>

            <!-- Current Amount Display -->
            <div class="current-amount">
                <div class="amount-label">💰 Total Tabungan</div>
                <div class="amount-value" id="currentAmount">Rp 0</div>
            </div>
        </div>

        <div class="main-content">
            <!-- Horizontal Divider -->
            <div class="divider"></div>

            <!-- Input Section -->
            <div class="input-section">
                <input 
                    type="number" 
                    id="amountInput" 
                    class="input-field" 
                    placeholder="Masukkan jumlah tabungan..."
                    min="1"
                >
                <button class="add-btn" onclick="addSavings()">Tambahkan</button>
            </div>
            <div class="error-message" id="errorMessage">Silakan masukkan jumlah yang valid!</div>

            <!-- History Section -->
            <div class="history-section">
                <h3>
                    <div class="history-header">
                        <span>📊 Riwayat Menabung</span>
                    </div>
                    <button class="reset-btn" onclick="resetAllData()">🗑️ Reset Semua</button>
                </h3>
                <div id="historyList" class="history-list">
                    <div class="no-history">Belum ada riwayat menabung</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Calculator Button -->
    <button class="calculator-btn" onclick="openCalculator()" title="Kalkulator">🧮</button>

    <!-- Calculator Modal -->
    <div id="calculatorModal" class="calculator-modal">
        <div class="calculator">
            <button class="close-calculator" onclick="closeCalculator()">&times;</button>
            <div class="calculator-header">🧮 Kalkulator</div>
            <input type="text" class="calculator-display" id="calcDisplay" readonly>
            <div class="calculator-buttons">
                <button class="calc-btn clear" onclick="clearCalculator()">C</button>
                <button class="calc-btn clear" onclick="deleteLast()">⌫</button>
                <button class="calc-btn operator" onclick="appendToDisplay('/')">/</button>
                <button class="calc-btn operator" onclick="appendToDisplay('*')">×</button>
                
                <button class="calc-btn number" onclick="appendToDisplay('7')">7</button>
                <button class="calc-btn number" onclick="appendToDisplay('8')">8</button>
                <button class="calc-btn number" onclick="appendToDisplay('9')">9</button>
                <button class="calc-btn operator" onclick="appendToDisplay('-')">-</button>
                
                <button class="calc-btn number" onclick="appendToDisplay('4')">4</button>
                <button class="calc-btn number" onclick="appendToDisplay('5')">5</button>
                <button class="calc-btn number" onclick="appendToDisplay('6')">6</button>
                <button class="calc-btn operator" onclick="appendToDisplay('+')">+</button>
                
                <button class="calc-btn number" onclick="appendToDisplay('1')">1</button>
                <button class="calc-btn number" onclick="appendToDisplay('2')">2</button>
                <button class="calc-btn number" onclick="appendToDisplay('3')">3</button>
                <button class="calc-btn equals" onclick="calculate()" style="grid-row: span 2;">=</button>
                
                <button class="calc-btn number" onclick="appendToDisplay('0')" style="grid-column: span 2;">0</button>
                <button class="calc-btn number" onclick="appendToDisplay('.')">.</button>
            </div>
            <button class="use-result-btn" id="useResultBtn" onclick="useCalculatorResult()" disabled>
                Gunakan Hasil untuk Tabungan
            </button>
        </div>
    </div>

    <script>
        // Data storage
        let savingsData = {
            name: 'Nama Anda',
            goal: 'Tujuan Menabung',
            currentAmount: 0,
            history: []
        };

        let calculatorResult = null;

        // Load data from localStorage on page load
        function loadSavedData() {
            const savedData = localStorage.getItem('savingsData');
            if (savedData) {
                try {
                    savingsData = JSON.parse(savedData);
                    updateDisplay();
                } catch (error) {
                    console.error('Error loading saved data:', error);
                }
            }
        }

        // Save data to localStorage
        function saveData() {
            localStorage.setItem('savingsData', JSON.stringify(savingsData));
        }

        // Update display with current data
        function updateDisplay() {
            document.getElementById('nameText').textContent = savingsData.name;
            document.getElementById('goalText').textContent = '🎯 ' + savingsData.goal;
            document.getElementById('currentAmount').textContent = 'Rp ' + formatCurrency(savingsData.currentAmount);
            updateHistoryList();
        }

        // Format currency
        function formatCurrency(amount) {
            return new Intl.NumberFormat('id-ID').format(amount);
        }

        // Name editing functions
        function editName() {
            document.getElementById('nameDisplay').style.display = 'none';
            document.getElementById('nameInput').style.display = 'flex';
            document.getElementById('nameField').value = savingsData.name;
            document.getElementById('nameField').focus();
        }

        function saveName() {
            const newName = document.getElementById('nameField').value.trim();
            if (newName) {
                savingsData.name = newName;
                saveData();
                updateDisplay();
            }
            cancelEditName();
        }

        function cancelEditName() {
            document.getElementById('nameDisplay').style.display = 'flex';
            document.getElementById('nameInput').style.display = 'none';
        }

        // Goal editing functions
        function editGoal() {
            document.getElementById('goalDisplay').style.display = 'none';
            document.getElementById('goalInput').style.display = 'flex';
            document.getElementById('goalField').value = savingsData.goal;
            document.getElementById('goalField').focus();
        }

        function saveGoal() {
            const newGoal = document.getElementById('goalField').value.trim();
            if (newGoal) {
                savingsData.goal = newGoal;
                saveData();
                updateDisplay();
            }
            cancelEditGoal();
        }

        function cancelEditGoal() {
            document.getElementById('goalDisplay').style.display = 'flex';
            document.getElementById('goalInput').style.display = 'none';
        }

        // Add savings function
        function addSavings() {
            const amountInput = document.getElementById('amountInput');
            const errorMessage = document.getElementById('errorMessage');
            const amount = parseFloat(amountInput.value);

            // Reset error message
            errorMessage.style.display = 'none';
            amountInput.style.borderColor = '#e0e0e0';

            // Validate input
            if (isNaN(amount) || amount <= 0) {
                errorMessage.style.display = 'block';
                amountInput.style.borderColor = '#f44336';
                amountInput.focus();
                return;
            }

            // Add to current amount
            savingsData.currentAmount += amount;

            // Add to history
            const now = new Date();
            const historyItem = {
                id: Date.now().toString(),
                amount: amount,
                date: now.toLocaleString('id-ID', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                })
            };
            
            savingsData.history.unshift(historyItem);
            
            // Save and update display
            saveData();
            updateDisplay();

            // Reset input
            amountInput.value = '';

            // Success animation
            const amountElement = document.getElementById('currentAmount');
            amountElement.style.transform = 'scale(1.1)';
            amountElement.style.transition = 'transform 0.3s ease';
            setTimeout(() => {
                amountElement.style.transform = 'scale(1)';
            }, 300);
        }

        // Update history list
        function updateHistoryList() {
            const historyList = document.getElementById('historyList');
            
            if (savingsData.history.length === 0) {
                historyList.innerHTML = '<div class="no-history">Belum ada riwayat menabung</div>';
                return;
            }

            let historyHTML = '';
            savingsData.history.forEach(item => {
                historyHTML += `
                    <div class="history-item">
                        <div>
                            <div class="history-date">${item.date}</div>
                        </div>
                        <div class="history-amount">+Rp ${formatCurrency(item.amount)}</div>
                        <button class="delete-btn" onclick="deleteHistoryItem('${item.id}')">🗑️</button>
                    </div>
                `;
            });
            
            historyList.innerHTML = historyHTML;
        }

        // Delete history item
        function deleteHistoryItem(id) {
            const item = savingsData.history.find(h => h.id === id);
            if (item && confirm(`Hapus tabungan Rp ${formatCurrency(item.amount)}?`)) {
                savingsData.currentAmount -= item.amount;
                savingsData.history = savingsData.history.filter(h => h.id !== id);
                saveData();
                updateDisplay();
            }
        }

        // Reset all data
        function resetAllData() {
            if (confirm('Apakah Anda yakin ingin menghapus semua data tabungan?')) {
                savingsData = {
                    name: 'Nama Anda',
                    goal: 'Tujuan Menabung',
                    currentAmount: 0,
                    history: []
                };
                saveData();
                updateDisplay();
            }
        }

        // Calculator functions
        function openCalculator() {
            document.getElementById('calculatorModal').style.display = 'flex';
            clearCalculator();
        }

        function closeCalculator() {
            document.getElementById('calculatorModal').style.display = 'none';
        }

        function appendToDisplay(value) {
            const display = document.getElementById('calcDisplay');
            if (display.value === '0' && value !== '.') {
                display.value = value;
            } else {
                display.value += value;
            }
            updateUseResultButton();
        }

        function clearCalculator() {
            document.getElementById('calcDisplay').value = '';
            calculatorResult = null;
            updateUseResultButton();
        }

        function deleteLast() {
            const display = document.getElementById('calcDisplay');
            display.value = display.value.slice(0, -1);
            updateUseResultButton();
        }

        function calculate() {
            const display = document.getElementById('calcDisplay');
            try {
                const expression = display.value.replace(/×/g, '*');
                const result = eval(expression);
                
                if (isFinite(result)) {
                    display.value = result;
                    calculatorResult = Math.abs(result);
                    updateUseResultButton();
                } else {
                    display.value = 'Error';
                    calculatorResult = null;
                    updateUseResultButton();
                }
            } catch (error) {
                display.value = 'Error';
                calculatorResult = null;
                updateUseResultButton();
            }
        }

        function updateUseResultButton() {
            const btn = document.getElementById('useResultBtn');
            
            if (calculatorResult && calculatorResult > 0 && !isNaN(calculatorResult)) {
                btn.disabled = false;
                btn.textContent = `Gunakan Rp ${formatCurrency(calculatorResult)} untuk Tabungan`;
            } else {
                btn.disabled = true;
                btn.textContent = 'Gunakan Hasil untuk Tabungan';
            }
        }

        function useCalculatorResult() {
            if (calculatorResult && calculatorResult > 0) {
                document.getElementById('amountInput').value = calculatorResult;
                closeCalculator();
                document.getElementById('amountInput').focus();
            }
        }

        // Event listeners
        document.addEventListener('DOMContentLoaded', function() {
            loadSavedData();
            
            // Enter key support for inputs
            document.getElementById('amountInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    addSavings();
                }
            });

            document.getElementById('nameField').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    saveName();
                } else if (e.key === 'Escape') {
                    cancelEditName();
                }
            });

            document.getElementById('goalField').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    saveGoal();
                } else if (e.key === 'Escape') {
                    cancelEditGoal();
                }
            });

            // Close calculator when clicking outside
            document.getElementById('calculatorModal').addEventListener('click', function(e) {
                if (e.target === this) {
                    closeCalculator();
                }
            });

            // Calculator keyboard support
            document.addEventListener('keydown', function(e) {
                const modal = document.getElementById('calculatorModal');
                if (modal.style.display === 'flex') {
                    const key = e.key;
                    if ('0123456789+-*/.'.includes(key)) {
                        e.preventDefault();
                        const displayKey = key === '*' ? '×' : key;
                        appendToDisplay(displayKey);
                    } else if (key === 'Enter' || key === '=') {
                        e.preventDefault();
                        calculate();
                    } else if (key === 'Escape') {
                        e.preventDefault();
                        closeCalculator();
                    } else if (key === 'Backspace') {
                        e.preventDefault();
                        deleteLast();
                    } else if (key === 'Delete' || key.toLowerCase() === 'c') {
                        e.preventDefault();
                        clearCalculator();
                    }
                }
            });
        });
    </script>
</body>
</html>
