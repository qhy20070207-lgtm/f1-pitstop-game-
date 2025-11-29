// 1. 获取所有需要的DOM元素
const startButton = document.getElementById('startButton');
const timerDisplay = document.getElementById('timer');
const statusDisplay = document.getElementById('status');
const resultDisplay = document.getElementById('result');

// 所有轮胎的ID列表
const wheelIds = ['wheel-FL', 'wheel-FR', 'wheel-RL', 'wheel-RR'];
// 存储所有轮胎的DOM元素
const wheels = wheelIds.map(id => document.getElementById(id)); 

// 2. 游戏状态变量
let isGameRunning = false;
let startTime = 0;
let timerInterval = null;
let currentWheelIndex = 0;
let wheelsToComplete = []; // 存储随机的轮胎点击顺序

// 3. 游戏计时器函数
function updateTimer() {
    if (!isGameRunning) return;

    const currentTime = Date.now();
    const elapsedTime = (currentTime - startTime) / 1000; // 转换为秒
    timerDisplay.textContent = `时间: ${elapsedTime.toFixed(3)} 秒`; // 显示到毫秒
}

// 4. 游戏开始函数
function startGame() {
    if (isGameRunning) return;

    // 重置状态
    isGameRunning = true;
    currentWheelIndex = 0;
    resultDisplay.textContent = '';
    
    // 清除所有轮胎的活动状态
    wheels.forEach(wheel => {
        wheel.classList.remove('wheel-active');
        wheel.textContent = wheel.id.split('-')[1].toUpperCase(); // 恢复初始文本
    });
    
    // 随机化换胎顺序 (关键步骤)
    // 复制数组并进行洗牌（Fisher-Yates算法简化）
    wheelsToComplete = [...wheelIds].sort(() => Math.random() - 0.5);

    // 设置状态信息
    statusDisplay.textContent = '进站中... 请按顺序点击轮胎!';
    startButton.disabled = true; // 禁用开始按钮

    // 开始计时
    startTime = Date.now();
    timerInterval = setInterval(updateTimer, 10); // 每10毫秒更新一次计时器

    // 激活第一个轮胎
    activateNextWheel();
}

// 5. 激活下一个需要点击的轮胎
function activateNextWheel() {
    if (currentWheelIndex >= wheelsToComplete.length) {
        // 所有轮胎已完成
        endGame();
        return;
    }

    // 获取当前需要激活的轮胎ID
    const nextWheelId = wheelsToComplete[currentWheelIndex];
    const nextWheel = document.getElementById(nextWheelId);

    // 激活它
    nextWheel.classList.add('wheel-active');
    nextWheel.textContent = '扳手!'; // 提示玩家点击
}

// 6. 游戏结束函数
function endGame() {
    isGameRunning = false;
    clearInterval(timerInterval); // 停止计时
    startButton.disabled = false; // 重新启用开始按钮

    const finalTime = ((Date.now() - startTime) / 1000).toFixed(3);

    statusDisplay.textContent = `恭喜! 进站完成!`;
    resultDisplay.innerHTML = `总时间：<span style="color: #e10600;">${finalTime} 秒</span>`;
}

// 7. 轮胎点击事件处理函数
function handleWheelClick(event) {
    if (!isGameRunning) return;

    const clickedWheelId = event.target.id;
    const requiredWheelId = wheelsToComplete[currentWheelIndex];

    if (clickedWheelId === requiredWheelId) {
        // 成功点击了正确的轮胎
        
        // 1. 完成当前轮胎的操作（视觉反馈）
        event.target.classList.remove('wheel-active');
        event.target.textContent = 'OK'; // 显示完成
        
        // 2. 移动到下一个轮胎
        currentWheelIndex++;
        
        // 3. 激活下一个轮胎或结束游戏
        activateNextWheel();

    } else {
        // 点击了错误的轮胎 - 增加惩罚 (简单惩罚：重新开始本轮，或时间惩罚)
        // 我们这里选择一个简单的惩罚：显示错误并清空当前操作的轮胎状态，让玩家重试
        statusDisplay.textContent = '错误! 点击了错误的轮胎! 请重新开始!';
        endGame();
        
        // 可以在这里加上时间惩罚，例如：
        // startTime -= 1000; // 罚时1秒
    }
}


// 8. 初始化：给按钮和所有轮胎添加事件监听器
startButton.addEventListener('click', startGame);

wheels.forEach(wheel => {
    wheel.addEventListener('click', handleWheelClick);
});

// 初始化时隐藏轮胎文本
wheels.forEach(wheel => {
    wheel.textContent = wheel.id.split('-')[1].toUpperCase();
    wheel.style.opacity = 1; // 确保初始可见
});
