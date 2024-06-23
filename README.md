![](https://img.shields.io/github/stars/hsiangfeng/README-Example-Template.svg)｜![](https://img.shields.io/github/forks/hsiangfeng/README-Example-Template.svg)｜![](https://img.shields.io/github/issues-pr/hsiangfeng/README-Example-Template.svg)｜![](https://img.shields.io/github/issues/hsiangfeng/README-Example-Template.svg)

# Butter Noise Fliter 奶油聲音過濾器

## Introduction 簡介
This repository provides a simple example and demonstration of a Butterworth filter in Python, particularly for audio with a complicated background. To avoid environment issues, the main body of code was built on Google Colab, allowing it to run smoothly without any pre-construction.

本專案提供了一個用 Python 實現的 Butterworth 濾波器的簡單示例和演示，特別適用於處理背景複雜的音頻。為了使程式碼運行更加簡單，所有的內容將在 Google Colab 上實現，所以不需要做環境上的調整。

## Result 成果展示
Input: YouTube URL (or apply Default) Output: org_audio.mpe(original audio) processed_audio.mp3（processed audio）

輸入：YouTube 網址（亦可以使用 Default）輸出：org_audio.mpe（紀錄原始音訊）processed_audio.mp3（處理後的音訊）

<img src="https://github.com/E84081210/Test/blob/main/Result/5.0_result.png" alt="專案封面圖" width="80%">

Top image: waveform of the original audio. Bottom image: waveform of the processed audio. The audio quality shows noticeable differences, especially in the reduced background noise and the highlighted vocals. However, the processed audio sounds noticeably thinner.

圖片上方：原始音訊的波形圖。圖片下方：處理後的音訊波形圖。音訊的品質有很明顯的差異，特別是在背景噪音降低和人聲凸顯的部分，不過，處理後的音訊明顯比較單薄。

## Iteration 版本迭代

### :one: 第一版
In version I, an arbitrary audio signal was used for preliminary algorithm testing. However, the results were relatively unsatisfactory, with significant degradation in audio quality.
在版本 I 中，我使用了隨機音頻信號進行初步的算法測試。然而，結果非常不理解，音質顯著地下降了。

```python
# Generate simulated data
np.random.seed(0)
fs = 8000  # Sampling rate
t = np.linspace(0, 1, fs, endpoint=False)
desired_signal = np.sin(2 * np.pi * 300 * t)  # Simulated desired audio signal
noise = 0.5 * np.random.normal(size=t.shape)  # Simulated noise
received_signal = desired_signal + noise  # Signal received by microphone

# LMS filter implementation
def lms_filter(received_signal, desired_signal, mu, num_taps):
    n = len(received_signal)
    h = np.zeros(num_taps)  # Filter weights initialization
    output = np.zeros(n)  # Output signal
    error = np.zeros(n)  # Error signal
    
    for i in range(num_taps, n):
        x = received_signal[i:i-num_taps:-1]
        y = np.dot(h, x)
        error[i] = desired_signal[i] - y
        h = h + 2 * mu * error[i] * x
        output[i] = y
    
    return output, error, h

# Set LMS filter parameters
mu = 0.01  # Learning rate
num_taps = 32  # Number of filter coefficients

# Apply LMS filter
output_signal, error_signal, filter_weights = lms_filter(received_signal, desired_signal, mu, num_taps)
```





## 畫面

> 可提供 1~3 張圖片，讓觀看者透過 README 了解整體畫面

![範例圖片 1](https://fakeimg.pl/500/)
![範例圖片 2](https://fakeimg.pl/500/)
![範例圖片 3](https://fakeimg.pl/500/)

## 安裝

> 請務必依據你的專案來調整內容。

以下將會引導你如何安裝此專案到你的電腦上。

Node.js 版本建議為：`16.15.0` 以上...

### 取得專案

```bash
git clone git@github.com:hsiangfeng/README-Example-Template.git
```

### 移動到專案內

```bash
cd README-Example-Template
```

### 安裝套件

```bash
npm install
```

### 環境變數設定

請在終端機輸入 `cp .env.example .env` 來複製 .env.example 檔案，並依據 `.env` 內容調整相關欄位。

### 運行專案

```bash
npm run serve
```

### 開啟專案

在瀏覽器網址列輸入以下即可看到畫面

```bash
http://localhost:8080/
```

## 環境變數說明

```env
APIPATH= # API 位置
COUSTOMPATH= # 自訂變數
...
```

## 資料夾說明

- views - 畫面放置處
- controllers - 控制器放置處
- modules - 模組放置處
- assets - 靜態資源放置處
  - scss - scss 檔案放置處
  - images - 圖片放置處
...

## 專案技術

- Node.js v16.15.0
- Vue v3.2.20
- Vite v4.0.4
- Vue Router v4.0.11
- Axios v0.24.0
- Bootstrap v5.1.3
...

## 第三方服務

- Algolia
- Google Analytics
...

## CI/CD 說明

此專案有使用 Github Actions，所以發起 PR 時會自動執行以下動作：

- 建立 Node.js 環境
- 安裝相依套件
- 編譯程式碼
- 執行 ESLint 掃描
- 執行測試
...

當專案 merge 到 main 時會自動執行以下動作：

- 建立 Node.js 環境
- 安裝相依套件
- 編譯程式碼
- 執行 ESLint 掃描
- 執行測試
- 部署到 Github Pages
...


