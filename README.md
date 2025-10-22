# hugs-icon-generator
<!DOCTYPE html>

<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>hugs - アイコン生成プロトタイプ</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
      background: #f8f8f8;
      color: #000;
      padding: 20px;
    }
    .container {
      max-width: 900px;
      margin: 0 auto;
      background: #fff;
      padding: 40px;
    }

```
h1 {
  font-size: 32px;
  font-weight: 600;
  margin-bottom: 8px;
  letter-spacing: 0.5px;
}
.subtitle {
  font-size: 14px;
  color: #666;
  margin-bottom: 40px;
}

/* API Key入力 */
.api-section {
  margin-bottom: 32px;
  padding: 20px;
  background: #fafafa;
  border: 1px solid #e5e5e5;
}
.api-label {
  font-size: 12px;
  font-weight: 600;
  color: #666;
  margin-bottom: 8px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.api-input {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #e5e5e5;
  font-size: 14px;
  font-family: 'Courier New', monospace;
}
.api-help {
  font-size: 12px;
  color: #999;
  margin-top: 8px;
  line-height: 1.5;
}
.api-help a {
  color: #000;
  text-decoration: underline;
}

/* アップロードセクション */
.upload-section {
  margin-bottom: 32px;
}
.section-title {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 16px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.upload-area {
  border: 2px dashed #999;
  padding: 40px;
  text-align: center;
  background: #fafafa;
  cursor: pointer;
  transition: all 0.2s;
}
.upload-area:hover {
  border-color: #000;
  background: #f0f0f0;
}
.upload-area.dragover {
  border-color: #000;
  background: #e8e8e8;
}
.upload-icon {
  font-size: 48px;
  margin-bottom: 16px;
}
.upload-text {
  font-size: 14px;
  color: #666;
  margin-bottom: 16px;
}
.file-input {
  display: none;
}
.upload-btn {
  padding: 12px 24px;
  background: #000;
  color: #fff;
  border: none;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.upload-btn:hover {
  background: #333;
}

/* プレビューセクション */
.preview-section {
  margin-bottom: 32px;
}
.original-preview {
  max-width: 300px;
  margin: 0 auto;
}
.original-preview img {
  width: 100%;
  height: auto;
  border: 1px solid #e5e5e5;
}
.preview-info {
  text-align: center;
  margin-top: 12px;
  font-size: 13px;
  color: #666;
}

/* 生成ボタン */
.generate-section {
  margin-bottom: 40px;
  text-align: center;
}
.generate-btn {
  padding: 16px 48px;
  background: #000;
  color: #fff;
  border: none;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  transition: all 0.2s;
}
.generate-btn:hover {
  background: #333;
}
.generate-btn:disabled {
  background: #ddd;
  color: #999;
  cursor: not-allowed;
}

/* 結果セクション */
.results-section {
  display: none;
}
.results-section.show {
  display: block;
}
.results-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 20px;
  margin-top: 20px;
}
.result-item {
  text-align: center;
}
.result-label {
  font-size: 11px;
  color: #666;
  margin-bottom: 8px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.result-emoji {
  font-size: 24px;
  margin-left: 8px;
}
.result-image-container {
  width: 100%;
  aspect-ratio: 1;
  background: #f0f0f0;
  border: 1px solid #e5e5e5;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 12px;
  overflow: hidden;
}
.result-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.loading {
  font-size: 14px;
  color: #999;
  animation: pulse 1.5s ease-in-out infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
.download-btn {
  padding: 8px 16px;
  background: #fff;
  border: 1px solid #000;
  font-size: 12px;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  transition: all 0.2s;
}
.download-btn:hover {
  background: #000;
  color: #fff;
}

/* エラー表示 */
.error-message {
  padding: 16px;
  background: #fee;
  border: 1px solid #fcc;
  color: #c00;
  margin: 20px 0;
  font-size: 14px;
  display: none;
}
.error-message.show {
  display: block;
}

/* ステータス */
.status-message {
  text-align: center;
  padding: 16px;
  background: #f0f0f0;
  margin: 20px 0;
  font-size: 14px;
  color: #666;
}
```

  </style>
</head>
<body>
  <div class="container">
    <h1>hugs</h1>
    <div class="subtitle">アイコン生成プロトタイプ - Nano Banana API テスト</div>

```
<!-- API Key入力 -->
<div class="api-section">
  <div class="api-label">Gemini API Key</div>
  <input 
    type="password" 
    id="apiKey" 
    class="api-input" 
    placeholder="AIza..."
    autocomplete="off"
  >
  <div class="api-help">
    Google AI Studioで取得できます: 
    <a href="https://aistudio.google.com/app/apikey" target="_blank">API Keyを取得</a>
    <br>入力したAPIキーはブラウザに保存されません（セキュア）
  </div>
</div>

<!-- アップロードセクション -->
<div class="upload-section">
  <div class="section-title">1. 犬の写真をアップロード</div>
  <div class="upload-area" id="uploadArea">
    <div class="upload-icon">📷</div>
    <div class="upload-text">
      クリックして写真を選択<br>
      または<br>
      ドラッグ&ドロップ
    </div>
    <button class="upload-btn" onclick="document.getElementById('fileInput').click()">
      写真を選択
    </button>
  </div>
  <input 
    type="file" 
    id="fileInput" 
    class="file-input" 
    accept="image/*"
  >
</div>

<!-- プレビュー -->
<div class="preview-section" id="previewSection" style="display: none;">
  <div class="section-title">アップロードした写真</div>
  <div class="original-preview">
    <img id="previewImage" src="" alt="プレビュー">
    <div class="preview-info" id="previewInfo"></div>
  </div>
</div>

<!-- 生成ボタン -->
<div class="generate-section">
  <button class="generate-btn" id="generateBtn" disabled>
    アイコンを生成
  </button>
</div>

<!-- エラーメッセージ -->
<div class="error-message" id="errorMessage"></div>

<!-- ステータス -->
<div class="status-message" id="statusMessage" style="display: none;"></div>

<!-- 結果 -->
<div class="results-section" id="resultsSection">
  <div class="section-title">2. 生成されたアイコン（5種類）</div>
  <div class="results-grid">
    <div class="result-item">
      <div class="result-label">喜び <span class="result-emoji">😊</span></div>
      <div class="result-image-container" id="result-happy">
        <div class="loading">生成中...</div>
      </div>
      <button class="download-btn" onclick="downloadIcon('happy')" style="display: none;">Download</button>
    </div>
    
    <div class="result-item">
      <div class="result-label">興奮 <span class="result-emoji">🤩</span></div>
      <div class="result-image-container" id="result-excited">
        <div class="loading">生成中...</div>
      </div>
      <button class="download-btn" onclick="downloadIcon('excited')" style="display: none;">Download</button>
    </div>
    
    <div class="result-item">
      <div class="result-label">普通 <span class="result-emoji">😐</span></div>
      <div class="result-image-container" id="result-neutral">
        <div class="loading">生成中...</div>
      </div>
      <button class="download-btn" onclick="downloadIcon('neutral')" style="display: none;">Download</button>
    </div>
    
    <div class="result-item">
      <div class="result-label">悲しみ <span class="result-emoji">😢</span></div>
      <div class="result-image-container" id="result-sad">
        <div class="loading">生成中...</div>
      </div>
      <button class="download-btn" onclick="downloadIcon('sad')" style="display: none;">Download</button>
    </div>
    
    <div class="result-item">
      <div class="result-label">疲れ <span class="result-emoji">😴</span></div>
      <div class="result-image-container" id="result-tired">
        <div class="loading">生成中...</div>
      </div>
      <button class="download-btn" onclick="downloadIcon('tired')" style="display: none;">Download</button>
    </div>
  </div>
</div>
```

  </div>

  <script>
    // 統一プロンプト定義
    const BASE_STYLE = `Transform this dog photo into a minimalist line art icon with these EXACT specifications:

STYLE REQUIREMENTS (CRITICAL - DO NOT DEVIATE):
- Thin, clean black outline style (1-2px lines)
- Simple, hand-drawn aesthetic with smooth curves
- Minimalist facial features: small dot eyes, simple nose
- Solid fill colors (white, gray, or the dog's main coat color)
- Monochrome or very limited color palette (max 2-3 colors)
- Rounded, friendly shapes
- Clean, icon-friendly design
- White or transparent background
- Centered head portrait composition
- Focus on face only, minimal body

MUST MAINTAIN FROM ORIGINAL:
- Dog breed characteristics (ear shape, face proportions)
- Coat color (simplified to solid tones)
- Overall face shape

OUTPUT FORMAT:
- 512x512px
- Icon-suitable simplicity
- Consistent with other icons in the set`;

    const EXPRESSIONS = {
      happy: {
        name: '喜び',
        emoji: '😊',
        prompt: `${BASE_STYLE}

EXPRESSION: Happy and joyful
- Tongue slightly out
- Eyes: simple happy dots or curves
- Slight smile indicated by mouth curve
- Relaxed, friendly appearance`
      },
      excited: {
        name: '興奮',
        emoji: '🤩',
        prompt: `${BASE_STYLE}

EXPRESSION: Excited and energetic
- Wide open mouth, big smile
- Eyes: large dots or sparkles
- Ears perked up if applicable
- Dynamic, enthusiastic energy`
      },
      neutral: {
        name: '普通',
        emoji: '😐',
        prompt: `${BASE_STYLE}

EXPRESSION: Calm and neutral
- Closed or relaxed mouth
- Eyes: simple dots, neutral gaze
- Neutral ear position
- Peaceful, calm demeanor`
      },
      sad: {
        name: '悲しみ',
        emoji: '😢',
        prompt: `${BASE_STYLE}

EXPRESSION: Sad and downcast
- Droopy or downturned eyes
- Slightly lowered ears if applicable
- Small, closed mouth
- Gentle, melancholic feeling`
      },
      tired: {
        name: '疲れ',
        emoji: '😴',
        prompt: `${BASE_STYLE}

EXPRESSION: Sleepy and tired
- Half-closed or sleepy eyes (horizontal lines)
- Relaxed, droopy features
- Mouth closed or slightly open
- Calm, drowsy appearance`
      }
    };
    
    let uploadedImageBase64 = null;
    let generatedIcons = {};
    
    // DOM要素
    const apiKeyInput = document.getElementById('apiKey');
    const uploadArea = document.getElementById('uploadArea');
    const fileInput = document.getElementById('fileInput');
    const previewSection = document.getElementById('previewSection');
    const previewImage = document.getElementById('previewImage');
    const previewInfo = document.getElementById('previewInfo');
    const generateBtn = document.getElementById('generateBtn');
    const resultsSection = document.getElementById('resultsSection');
    const errorMessage = document.getElementById('errorMessage');
    const statusMessage = document.getElementById('statusMessage');
    
    // ドラッグ&ドロップ
    uploadArea.addEventListener('dragover', (e) => {
      e.preventDefault();
      uploadArea.classList.add('dragover');
    });
    
    uploadArea.addEventListener('dragleave', () => {
      uploadArea.classList.remove('dragover');
    });
    
    uploadArea.addEventListener('drop', (e) => {
      e.preventDefault();
      uploadArea.classList.remove('dragover');
      const file = e.dataTransfer.files[0];
      if (file && file.type.startsWith('image/')) {
        handleFileUpload(file);
      }
    });
    
    uploadArea.addEventListener('click', () => {
      fileInput.click();
    });
    
    fileInput.addEventListener('change', (e) => {
      const file = e.target.files[0];
      if (file) {
        handleFileUpload(file);
      }
    });
    
    // ファイルアップロード処理
    function handleFileUpload(file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        const dataUrl = e.target.result;
        uploadedImageBase64 = dataUrl.split(',')[1]; // Base64部分のみ
        
        // プレビュー表示
        previewImage.src = dataUrl;
        previewInfo.textContent = `${file.name} (${(file.size / 1024).toFixed(1)} KB)`;
        previewSection.style.display = 'block';
        
        // 生成ボタン有効化
        checkGenerateButton();
      };
      reader.readAsDataURL(file);
    }
    
    // 生成ボタンの有効/無効チェック
    function checkGenerateButton() {
      const hasApiKey = apiKeyInput.value.trim().length > 0;
      const hasImage = uploadedImageBase64 !== null;
      generateBtn.disabled = !(hasApiKey && hasImage);
    }
    
    apiKeyInput.addEventListener('input', checkGenerateButton);
    
    // アイコン生成
    generateBtn.addEventListener('click', async () => {
      const apiKey = apiKeyInput.value.trim();
      
      if (!apiKey || !uploadedImageBase64) {
        showError('API KeyとMIと画像をアップロードしてください');
        return;
      }
      
      // UI更新
      generateBtn.disabled = true;
      generateBtn.textContent = '生成中...';
      resultsSection.classList.add('show');
      errorMessage.classList.remove('show');
      
      // 結果エリアをリセット
      for (const key of Object.keys(EXPRESSIONS)) {
        const container = document.getElementById(`result-${key}`);
        container.innerHTML = '<div class="loading">生成中...</div>';
      }
      
      try {
        // 各表情を順次生成
        let count = 0;
        for (const [key, config] of Object.entries(EXPRESSIONS)) {
          count++;
          showStatus(`アイコン生成中... (${count}/5) ${config.emoji} ${config.name}`);
          
          try {
            const imageData = await generateIcon(apiKey, config.prompt, uploadedImageBase64);
            
            // 結果を表示
            const container = document.getElementById(`result-${key}`);
            container.innerHTML = `<img src="data:image/png;base64,${imageData}" class="result-image" alt="${config.name}">`;
            
            // ダウンロードボタン表示
            container.parentElement.querySelector('.download-btn').style.display = 'inline-block';
            
            // 保存
            generatedIcons[key] = imageData;
            
            // APIレート制限対策
            await sleep(1500);
            
          } catch (error) {
            console.error(`Failed to generate ${key}:`, error);
            const container = document.getElementById(`result-${key}`);
            container.innerHTML = `<div style="color: #c00; font-size: 12px;">生成失敗</div>`;
          }
        }
        
        showStatus('✓ アイコン生成完了！');
        setTimeout(() => {
          statusMessage.style.display = 'none';
        }, 3000);
        
      } catch (error) {
        showError(`エラー: ${error.message}`);
      } finally {
        generateBtn.disabled = false;
        generateBtn.textContent = 'アイコンを生成';
      }
    });
    
    // Nano Banana APIを呼び出し
    async function generateIcon(apiKey, prompt, imageBase64) {
      try {
        const response = await fetch(
          'https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-image:generateContent',
          {
            method: 'POST',
            headers: {
              'x-goog-api-key': apiKey,
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              contents: [{
                parts: [
                  { text: prompt },
                  {
                    inline_data: {
                      mime_type: 'image/jpeg',
                      data: imageBase64
                    }
                  }
                ]
              }],
              generationConfig: {
                temperature: 0.3,
                topK: 40,
                topP: 0.95
              }
            })
          }
        );
        
        if (!response.ok) {
          const errorData = await response.json();
          console.error('API Error:', errorData);
          throw new Error(errorData.error?.message || `API Error: ${response.status}`);
        }
        
        const result = await response.json();
        console.log('API Response:', result);
        
        // レスポンス構造を確認
        if (!result.candidates || result.candidates.length === 0) {
          throw new Error('No candidates in response');
        }
        
        const candidate = result.candidates[0];
        
        // 画像データを抽出（複数のパターンに対応）
        let imageData = null;
        
        // パターン1: inline_data in parts
        if (candidate.content && candidate.content.parts) {
          const imagePart = candidate.content.parts.find(part => part.inline_data);
          if (imagePart) {
            imageData = imagePart.inline_data.data;
          }
        }
        
        // パターン2: 直接画像データがある場合
        if (!imageData && candidate.image) {
          imageData = candidate.image.data || candidate.image;
        }
        
        // パターン3: 他の構造
        if (!imageData && result.image) {
          imageData = result.image.data || result.image;
        }
        
        if (!imageData) {
          console.error('Response structure:', JSON.stringify(result, null, 2));
          throw new Error('画像データが見つかりませんでした。レスポンス構造を確認してください（コンソールログ参照）');
        }
        
        return imageData;
        
      } catch (error) {
        console.error('Generate Icon Error:', error);
        throw error;
      }
    }
    
    // ダウンロード
    function downloadIcon(type) {
      const imageData = generatedIcons[type];
      if (!imageData) return;
      
      const link = document.createElement('a');
      link.href = `data:image/png;base64,${imageData}`;
      link.download = `hugs-icon-${type}.png`;
      link.click();
    }
    
    // ヘルパー関数
    function showError(message) {
      errorMessage.textContent = message;
      errorMessage.classList.add('show');
    }
    
    function showStatus(message) {
      statusMessage.textContent = message;
      statusMessage.style.display = 'block';
    }
    
    function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
  </script>

</body>
</html>
