---
description: 選取並設定受影響的物件 (SybaseToSQL)
title: 選取及設定受影響的物件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 793430d548053b8d4c1cbf8dd07dd4e7d691c6d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468738"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>選取並設定受影響的物件 (SybaseToSQL)
在此頁面上，您可以選取資料表和外鍵，當 SSMA 確認上一個步驟中所選擇之物件的執行結果時，應該比較的變更。 此外，您也可以自訂驗證參數。  
  
## <a name="selection-of-affected-objects"></a>選取受影響的物件  
在位於視窗左側的 [Sybase] 物件樹狀結構中，檢查資料表和外鍵，應該比較的變更是否相同。  
  
如果 SSMA 測試人員無法驗證任何這些物件，您會看到標示為 **某些所選物件** 的連結在 [物件] 樹狀目錄下包含錯誤。 請按一下此連結來查看無法比較這些物件的原因，以及清除錯誤物件的選取專案。  
  
## <a name="table"></a>Table  
[資料表] 索引標籤包含所選資料表的格線視圖。 方格包含下列有關所選資料表的資訊：  
  
-   資料行名稱  
  
-   資料類型  
  
-   精確度  
  
-   調整  
  
-   規則  
  
-   預設  
  
-   身分識別  
  
-   Nullable  
  
## <a name="sql"></a>Sql  
[SQL] 索引標籤包含所選資料表的 [建立資料表] SQL。  
  
## <a name="data"></a>資料  
[資料] 索引標籤會顯示所選資料表中的資料。  
  
## <a name="properties"></a>屬性  
[屬性] 索引標籤會顯示選取之資料表的屬性。 [屬性] 索引標籤底下會出現下欄欄位：  
  
-   已建立或上次修改  
  
-   物件名稱  
  
## <a name="table-comparison-settings"></a>資料表比較設定  
在 [ **資料表比較** ] 頁面上建立資料表的比較規則。 您可以進行下列設定。  
  
### <a name="comparison-mode"></a>比較模式  
定義將執行比較的資料表內容。  
  
-   如果您只選取 [ **變更**]，將會執行資料表資料列的完整比較。  
  
-   如果您選取 [ **完整**]，則只會執行已變更之資料列的比較。  
  
## <a name="column-comparison-settings"></a>資料行比較設定  
在 [資料 **行比較** ] 頁面上建立資料表資料行的比較規則。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>在測試比較期間使用  
判斷此資料行是否會參與測試結果驗證。  
  
-   如果您選擇 [ **True**]，則在使用 SQL Server 中的資料行內容執行 Sybase 上的測試之後，SSMA 會比較此資料行的內容。
  
-   如果您選擇 [ **False**]，將會從結果驗證中排除資料行。  
  
### <a name="use-custom-scale"></a>使用自訂規模  
針對數值資料類型的資料行，您可以設定比較的自訂小數位數。  
  
-   如果您選擇 [ **True**]，將會根據 **比較比例** 值來舍入數值，再進行比較。  
  
-   如果您選擇 [ **False**]，數值比較將會是精確的。  
  
### <a name="comparing-scale"></a>比較尺規  
  
-   只有在 [ **使用自訂規模** ] 選項設定為 [ **True**] 時才能使用。 這是數值比較的有效位數。  
  
### <a name="date-time-comparing"></a>比較日期時間  
定義日期/時間值的比較方式。  
  
-   如果您選取 [ **比較整個日期**]，將會執行兩個平臺值的完整比較。  
  
-   如果您選取 [ **僅比較日期**]，將會忽略時間部分。  
  
-   如果您選取 [ **僅比較時間**]，將會忽略日期部分。  
  
-   如果您選取 [ **略過毫秒**]，將會比較最多幾秒鐘的結果。  
  
-   如果您選取 [ **忽略日期和毫秒**]，則只會依據時間部分來比較結果，並忽略第二個部分的小數部分。  
  
### <a name="ignore-strings-case"></a>忽略字串大小寫  
控制比較是否區分大小寫。  
  
-   如果您選擇 [ **True**]，則比較不區分大小寫。  
  
-   如果您選擇 [ **False**]，則比較會考慮字母大小寫。  
  
## <a name="comparing-sql"></a>比較 SQL  
您可以在 [ **比較 SQL** ] 頁面上查看 SSMA 測試人員所產生的 SELECT 語句。 測試人員將會逐列比較這些語句的結果集。 Sybase 結果集的每個下一個資料列都應等於所產生結果集的下一個資料列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
您可以編輯這些 SELECT 語句，以提供自訂驗證。 若要儲存 Sybase 和語句中的變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請使用**Apply**來源和目標 SQL 底下的 [套用] 按鈕。  
  
## <a name="next-step"></a>後續步驟  
[自訂呼叫順序 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[執行測試案例 &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[測試遷移的資料庫物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
