# 氣象格點觀測資料分析報告
## 1. **資料來源與前處理**
- 資料格式：原始 XML 以 67 × 120 的格點呈現，每格代表一筆攝氏溫度觀測值。
- 座標定義：左下角為東經 120.00°、北緯 21.88°；經緯度解析度皆為 0.03°。先沿經向填入 67 筆，再沿緯向堆疊 120 列。
- 資料清理：
將 -999. 標示的無效值轉為 NaN，
建立 temp_grid 方便繪製觀測熱度圖（Figure 1）。
![Figure_1](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%206.png)
### 1.1 **建立兩個資料集**：
* 分類：特徵 (lon_idx, lat_idx)，標籤為1/0。
* 回歸：僅保留有效觀測，目標為溫度值。
* 透過 StandardScaler 對特徵做 Z-score 標準化，並以 80/20 切分訓練與測試集；分類資料採 stratify 維持類別比例。
## 2. 模型設計
### 2.1 ClassificationNet
- 架構：Linear 2→128 → ReLU → Dropout 0.2 → Linear 128→64 → ReLU → Dropout 0.2 → Linear 64→32 → ReLU → Dropout 0.1 → Linear 32→1。
- 損失與最佳化：BCEWithLogitsLoss + Adam (lr=1e-3)。
- 訓練參數：批次 256，訓練 200 epoch。
### 2.2 RegressionNet
- 架構：Linear 2→128 → ReLU → Dropout 0.2 → Linear 128→128 → ReLU → Dropout 0.2 → Linear 128→32 → ReLU → Dropout 0.1 → Linear 32→1。
- 損失與最佳化：MSELoss + Adam (lr=1e-3)。
- 訓練參數：批次 256，訓練 300 epoch。

## 3. 訓練過程與結果分析
### 3.1 訓練歷程
- 分類：BCE 損失穩定下降；測試準確率自約 94% 逐步提昇並在 100 epoch 收斂於 98% 左右（Figure 2 左、右）。
  ![Figure_2](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy.png)
- 回歸：訓練 MSE 隨 epoch 持續下降，10 epoch 時趨於平穩（Figure 4 左）。
  ![Figure_2](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%203.png)
### 3.2 測試表現
| 指標	| ClassificationNet	| RegressionNet |
| ----- | --------- | -------- |
| Accuracy	| 0.982 |	– |
| MSE |	–	| 9.36 |
| RMSE	| –	| 3.06 °C | 
| MAE	| –	| 2.42 °C |
| R² |	–	| 0.87 |

* 混淆矩陣顯示對無效 (0) 與有效 (1) 樣本都有高辨識率（Figure 3）。  
![Figure_3](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image.png)
* 回歸模型的散點圖呈現大致沿對角線分布，殘差集中於 ±5°C 內，無明顯偏差（Figure 4 右）。
![Figure_3](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%205.png)
### 3.3 視覺化結果
- Figure 1：觀測溫度熱度圖（Spectral colormap），NaN 位置保留空白。  
  ![Figure_1](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%206.png)
- Figure 5：分類模型於完整網格上預測有效性（Dark2 colormap），清楚標示下架區域。  
  ![Figure_3](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%202.png)
- Figure 6：回歸模型在全網格補齊溫度預測，NaN 位置保留空白，提供地理對應的溫度分布。  
  ![Figure_1](https://github.com/xxx152/2025_machine_learning/blob/main/week4/img/image%20copy%204.png)
## 4. 討論與結論
- 資料轉換完整：成功從 XML 解析出 67×120 網格，將 -999. 轉為 NaN，並以經緯度解析度組成空間網格。
- 分類模型  
優點：準確率達 98%，可以看出本島位置。  
限制：離島沒辦法有效分類。
- 回歸模型  
優點：RMSE 3°C、R² 0.87，能大致看出溫度與地形的關係。  
限制：沒有很精確的預測，極端值無法預測。



