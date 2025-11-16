<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BMI健康评估系统</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
        }
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: #333;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .container {
            max-width: 900px;
            width: 100%;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        header {
            text-align: center;
            margin-bottom: 30px;
        }
        h1 {
            color: #2c3e50;
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        .subtitle {
            color: #7f8c8d;
            font-size: 1.2rem;
            margin-bottom: 20px;
        }
        .scenario {
            background-color: #e8f4fc;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 25px;
            border-left: 5px solid #3498db;
        }
        .scenario h2 {
            color: #2980b9;
            margin-bottom: 10px;
        }
        .content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }
        @media (max-width: 768px) {
            .content {
                grid-template-columns: 1fr;
            }
        }
        .card {
            background-color: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        .card h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #f1f2f6;
        }
        .input-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2c3e50;
        }
        input[type="number"] {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e1e8ed;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        input[type="number"]:focus {
            border-color: #3498db;
            outline: none;
        }
        button {
            background: linear-gradient(to right, #3498db, #2c3e50);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            margin-right: 10px;
            margin-bottom: 10px;
            transition: all 0.3s;
            box-shadow: 0 4px 6px rgba(50, 50, 93, 0.11), 0 1px 3px rgba(0, 0, 0, 0.08);
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 7px 14px rgba(50, 50, 93, 0.1), 0 3px 6px rgba(0, 0, 0, 0.08);
        }
        button:active {
            transform: translateY(1px);
        }
        button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
            background-color: #f8f9fa;
            display: none;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        th, td {
            border: 1px solid #e1e8ed;
            padding: 12px;
            text-align: center;
        }
        th {
            background-color: #3498db;
            color: white;
            font-weight: 600;
        }
        tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        .health-status {
            font-weight: bold;
            padding: 6px 12px;
            border-radius: 20px;
            display: inline-block;
        }
        .underweight {
            background-color: #f39c12;
            color: white;
        }
        .normal {
            background-color: #27ae60;
            color: white;
        }
        .overweight {
            background-color: #e74c3c;
            color: white;
        }
        .criteria {
            margin-top: 20px;
            padding: 15px;
            background-color: #e8f4fc;
            border-radius: 10px;
        }
        .criteria h4 {
            color: #2980b9;
            margin-bottom: 10px;
        }
        .criteria p {
            margin-bottom: 5px;
        }
        .weight-list {
            min-height: 100px;
            border: 2px dashed #bdc3c7;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            background-color: #f8f9fa;
            font-family: 'Courier New', monospace;
            font-size: 18px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .success-message {
            color: #27ae60;
            font-weight: bold;
            margin-top: 10px;
        }
        .error-message {
            color: #e74c3c;
            font-weight: bold;
            margin-top: 10px;
        }
        .programming-note {
            margin-top: 20px;
            padding: 15px;
            background-color: #2c3e50;
            color: white;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
        }
        .programming-note h4 {
            color: #3498db;
            margin-bottom: 10px;
        }
        .height-display {
            margin-top: 10px;
            padding: 10px;
            background-color: #e8f4fc;
            border-radius: 8px;
            font-weight: bold;
            display: none;
        }
        .section-title {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }
        .step-badge {
            background-color: #3498db;
            color: white;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 10px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>BMI计算与健康评估</h1>
            <p class="subtitle">使用编程思维解决实际问题</p>
        </header>
        
        <div class="scenario">
            <h2>学习情境</h2>
            <p>小申同学是个健身爱好者，形成了用数字化设备记录自己各项锻炼数据，监测体质数据的习惯。他记录了最近几天的体重数据，现在需要计算最近几天的BMI指数，并评估健康状况。</p>
        </div>
        
        <div class="content">
            <div class="card">
                <div class="section-title">
                    <div class="step-badge">1</div>
                    <h3>数据输入</h3>
                </div>
                
                <div class="input-group">
                    <label for="height">身高 (米):</label>
                    <input type="number" id="height" step="0.01" min="1.0" max="2.5" placeholder="例如：1.75">
                    <button id="submit-height">提交身高</button>
                </div>
                
                <div class="height-display" id="height-display">
                    <!-- 已提交的身高将显示在这里 -->
                </div>
                
                <div class="input-group">
                    <label for="weight-input">每日体重 (千克):</label>
                    <input type="number" id="weight-input" step="0.1" min="20" max="200" placeholder="例如：68.5" disabled>
                </div>
                
                <button id="add-weight" disabled>添加体重数据</button>
                <button id="clear-weights" disabled>清空体重列表</button>
                
                <div class="weight-list" id="weight-list-display">
                    weight = []
                </div>
                
                <button id="calculate" disabled>计算BMI并评估健康</button>
                
                <div class="programming-note">
                    <h4>编程提示</h4>
                    <p>1.weight.append(x)：在体重列表尾部追加数据x</p>
                    <p>2.使用while循环遍历体重列表</p>
                    <p>3.使用分支结构判断bmi健康状况</p>
               
                </div>
            </div>
            
            <div class="card">
                <div class="section-title">
                    <div class="step-badge">2</div>
                    <h3>结果与评估</h3>
                </div>
                
                <div class="result" id="result">
                    <table id="bmi-table">
                        <thead>
                            <tr>
                                <th>天数</th>
                                <th>体重 (kg)</th>
                                <th>BMI</th>
                                <th>健康状况</th>
                            </tr>
                        </thead>
                        <tbody id="bmi-results">
                            <!-- 结果将在这里显示 -->
                        </tbody>
                    </table>
                </div>
                
                <div class="criteria">
                    <h4>BMI判断标准</h4>
                    <p>BMI &lt; 18.5：<span class="health-status underweight">偏瘦</span></p>
                    <p>18.5 ≤ BMI ≤ 24.9：<span class="health-status normal">正常</span></p>
                    <p>BMI &gt; 24.9：<span class="health-status overweight">偏胖</span></p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 存储体重数据的数组
        let weightList = [];
        let submittedHeight = null;
        
        // 获取DOM元素
        const heightInput = document.getElementById('height');
        const submitHeightBtn = document.getElementById('submit-height');
        const heightDisplay = document.getElementById('height-display');
        const weightInput = document.getElementById('weight-input');
        const addWeightBtn = document.getElementById('add-weight');
        const clearWeightsBtn = document.getElementById('clear-weights');
        const weightListDisplay = document.getElementById('weight-list-display');
        const calculateBtn = document.getElementById('calculate');
        const resultDiv = document.getElementById('result');
        const bmiResults = document.getElementById('bmi-results');
        
        // 提交身高
        submitHeightBtn.addEventListener('click', function() {
            const height = parseFloat(heightInput.value);
            
            if (isNaN(height) || height <= 0) {
                showMessage('请输入有效的身高值！', 'error');
                return;
            }
            
            submittedHeight = height;
            heightDisplay.textContent = `已提交身高: ${height} 米`;
            heightDisplay.style.display = 'block';
            
            // 启用体重相关输入和按钮
            weightInput.disabled = false;
            addWeightBtn.disabled = false;
            clearWeightsBtn.disabled = false;
            
            showMessage('身高提交成功！现在可以添加体重数据。', 'success');
        });
        
        // 添加体重数据到列表
        addWeightBtn.addEventListener('click', function() {
            const weight = parseFloat(weightInput.value);
            
            if (isNaN(weight) || weight <= 0) {
                showMessage('请输入有效的体重值！', 'error');
                return;
            }
            
            weightList.push(weight);
            updateWeightListDisplay();
            weightInput.value = ''; // 清空输入框
            
            // 如果有体重数据，启用计算按钮
            if (weightList.length > 0) {
                calculateBtn.disabled = false;
            }
            
            showMessage('体重数据已添加！', 'success');
        });
        
        // 清空体重列表
        clearWeightsBtn.addEventListener('click', function() {
            weightList = [];
            updateWeightListDisplay();
            resultDiv.style.display = 'none';
            calculateBtn.disabled = true;
            showMessage('体重列表已清空！', 'success');
        });
        
        // 计算BMI
        calculateBtn.addEventListener('click', function() {
            if (submittedHeight === null) {
                showMessage('请先提交身高！', 'error');
                return;
            }
            
            if (weightList.length === 0) {
                showMessage('请先添加体重数据！', 'error');
                return;
            }
            
            calculateBMI(submittedHeight);
            showMessage('BMI计算完成！', 'success');
        });
        
        // 更新体重列表显示
        function updateWeightListDisplay() {
            if (weightList.length === 0) {
                weightListDisplay.textContent = 'weight = []';
            } else {
                weightListDisplay.textContent = 'weight = [' + weightList.join(', ') + ']';
            }
        }
        
        // 计算BMI并显示结果
        function calculateBMI(height) {
            // 清空之前的结果
            bmiResults.innerHTML = '';
            
            // 使用while循环遍历体重列表
            let i = 0;
            while (i < weightList.length) {
                // 计算BMI
                let bmi = weightList[i] / (height * height);
                
                // 判断健康状况
                let status, statusClass;
                if (bmi < 18.5) {
                    status = "偏瘦";
                    statusClass = "underweight";
                } else if (bmi <= 24.9) {
                    status = "正常";
                    statusClass = "normal";
                } else {
                    status = "偏胖";
                    statusClass = "overweight";
                }
                
                // 创建表格行
                const row = document.createElement('tr');
                
                // 添加天数单元格
                const dayCell = document.createElement('td');
                dayCell.textContent = i + 1;
                row.appendChild(dayCell);
                
                // 添加体重单元格
                const weightCell = document.createElement('td');
                weightCell.textContent = weightList[i];
                row.appendChild(weightCell);
                
                // 添加BMI单元格
                const bmiCell = document.createElement('td');
                bmiCell.textContent = bmi.toFixed(2);
                row.appendChild(bmiCell);
                
                // 添加健康状况单元格
                const statusCell = document.createElement('td');
                const statusSpan = document.createElement('span');
                statusSpan.textContent = status;
                statusSpan.className = `health-status ${statusClass}`;
                statusCell.appendChild(statusSpan);
                row.appendChild(statusCell);
                
                // 将行添加到表格
                bmiResults.appendChild(row);
                
                i++;
            }
            
            // 显示结果区域
            resultDiv.style.display = 'block';
        }
        
        // 显示消息
        function showMessage(message, type) {
            // 移除之前的消息
            const existingMessage = document.querySelector('.success-message, .error-message');
            if (existingMessage) {
                existingMessage.remove();
            }
            
            // 创建新消息
            const messageElement = document.createElement('div');
            messageElement.textContent = message;
            messageElement.className = type === 'success' ? 'success-message' : 'error-message';
            
            // 添加到按钮后面
            if (type === 'success') {
                calculateBtn.parentNode.insertBefore(messageElement, calculateBtn.nextSibling);
            } else {
                addWeightBtn.parentNode.insertBefore(messageElement, addWeightBtn.nextSibling);
            }
            
            // 3秒后自动移除
            setTimeout(() => {
                if (messageElement.parentNode) {
                    messageElement.remove();
                }
            }, 3000);
        }
    </script>
</body>
</html>
