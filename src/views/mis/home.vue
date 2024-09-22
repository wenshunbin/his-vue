<template>
    <div class="container">
      <div class="content">
        <div class="left-panel">
          <div class="title">神州大健康体检系统</div>
          <div class="info">医疗健康 模式创新</div>
          <div class="info">汇集名医 让诊疗更简单</div>
          <div class="features">
            <div class="feature blue">
              <span>1</span>
              <p>先进的技术</p>
            </div>
            <div class="feature red">
              <span>2</span>
              <p>强大的团队</p>
            </div>
            <div class="feature green">
              <span>3</span>
              <p>丰富的经验</p>
            </div>
          </div>
        </div>
        <div class="right-panel">
          <img src="../../assets/home/banner.png" alt="系统图示" class="system-image"/>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  .container {
    padding-top: 50px; /* 调整上内填充值，使内容向上移动 */
    display: flex;
    justify-content: center;
    align-items: flex-start; /* 更改为 flex-start 让内容向页面顶部对齐 */
    min-height: 100vh;
    background-color: #f5f7fa;
  }
  
  .content {
    display: flex;
    justify-content: space-between;
    width: 80%;
    max-width: 1200px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
    background-color: white;
    border-radius: 10px;
    overflow: hidden;
  }
  
  .left-panel {
    flex: 1;
    padding: 40px;
    text-align: center;
    background-color: #409eff;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  
  .title {
    font-size: 28px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .info {
    font-size: 18px;
    margin-bottom: 10px;
    line-height: 1.5;
  }
  
  .features {
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
  }
  
  .feature {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 120px;
    height: 120px;
    border-radius: 50%;
    color: white;
    font-size: 30px;
    font-weight: bold;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .feature:hover {
    transform: translateY(-10px);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  }
  
  .feature p {
    font-size: 14px;
    margin-top: 10px;
    font-weight: normal;
  }
  
  .blue {
    background-color: #1e90ff;
  }
  
  .red {
    background-color: #ff6347;
  }
  
  .green {
    background-color: #32cd32;
  }
  
  .right-panel {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }
  
  .system-image {
    max-width: 100%;
    height: auto;
    border-radius: 10px;
  }
  </style>
  