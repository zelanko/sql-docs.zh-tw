---
title: 選取並設定要測試的物件（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e0a8e7650534d50c5e5d7c3b02f2857764d9c2ca
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264645"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>選取及設定要測試的受影響物件 (OracleToSQL)
在此步驟中，您會選取要測試的物件，並設定比較程式的輸出參數和函數傳回值的設定。  
  
## <a name="selection-of-objects-to-test"></a>選取要測試的物件  
在位於視窗左側的 Oracle 物件樹狀結構中，檢查您想要在測試程式期間叫用的物件。 如 &#40;OracleToSQL&#41;主題，請參閱[測試遷移的資料庫物件](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)中的可測試物件完整清單。  
  
如果 SSMA 測試器不支援選取要測試的任何物件，您會在 [物件] 樹狀目錄底下看到標示為 [**某些選取的物件**] 的連結包含錯誤。 按一下此連結可查看無法測試這些物件的原因，以及清除錯誤物件的選取專案。  
  
在右側，您可以查看數個頁面： [ **SQL** ] 頁面會顯示目前物件的定義。 如果物件是預存程式或函式，[**參數**] 頁面會列出參數。 [**屬性**] 頁面會顯示物件的其他特性。 請參閱下面的**參數比較**和**呼叫值**的描述頁面。  
  
## <a name="parameter-comparison-settings"></a>參數比較設定  
在 [**參數比較**] 頁面中，建立輸出參數和傳回值的比較規則。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>在測試比較期間使用  
在 [測試結果比較] 中，使用選取的參數來啟用。  
  
-   如果您選擇 [ **True**]，SSMA 會在執行 Oracle 上的程式，並在 SQL Server 上使用對應的值，比較此參數的輸出值。
  
-   如果您選擇 [**False**]，則會從結果驗證中排除參數。  
  
### <a name="use-custom-scale"></a>使用自訂規模  
對於數值資料類型的參數，您可以設定比較的自訂縮放比例。  
  
-   如果您選擇 [ **True**]，則會在比較之前，根據**比較小**數位數值來進位數值。  
  
-   如果您選擇 [**False**]，數值比較將會是精確的。  
  
### <a name="comparing-scale"></a>比較尺規  
只有在 [**使用自訂調整**] 選項設定為 [ **True**] 時才可使用。 這是數值比較的有效位數。  
  
### <a name="date-time-comparing"></a>日期時間比較  
定義日期/時間值的比較方式。  
  
-   如果您選取 [**比較整個日期**]，將會執行兩個平臺之值的完整比較。  
  
-   如果您選取 [**僅比較日期**]，則會忽略時間部分。  
  
-   如果您選取 [**僅比較時間**]，則會忽略日期部分。  
  
-   如果您選取 [**略過毫秒**]，則會比較最多秒的結果。  
  
-   如果您選取 [**略過日期和毫秒**]，則只會根據時間部分比較結果，並忽略秒的小數部分。  
  
### <a name="ignore-strings-case"></a>忽略字串大小寫  
控制比較的區分大小寫。  
  
-   如果您選擇 [ **True**]，則比較不會區分大小寫。  
  
-   如果您選擇 [ **False**]，則比較會區分大小寫。  
  
### <a name="ignore-trailing-spaces"></a>忽略尾端空白  
控制在比較期間處理尾端空格的方式。  
  
-   如果您選擇**True**，比較的字串將會在比較之前先向右修剪。  
  
-   如果您選擇 [ **False**]，則比較的字串會保留尾端空白字元。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>指定程式和函式的輸入值（呼叫值）  
您可以在 [**呼叫值**] 頁面上指定輸入參數值。 [**新增呼叫**] 按鈕會新增具有空白參數值的呼叫。 [**移除呼叫**] 按鈕會移除目前的呼叫。  
  
## <a name="next-step"></a>後續步驟  
[選取並設定受影響的物件 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[&#40;OracleToSQL&#41;測試遷移的資料庫物件](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
