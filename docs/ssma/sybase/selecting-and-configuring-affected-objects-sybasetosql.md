---
title: 選取並設定受影響的物件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3aa7ccc8d559f7017fd2a9bf0bc20bc7ae191c46
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020995"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>選取並設定受影響的物件 (SybaseToSQL)
在此頁面中，您可以選取資料表和外鍵，當 SSMA 驗證在上一個步驟中所選物件的執行結果時，應該比較的變更。 此外，您也可以自訂驗證參數。  
  
## <a name="selection-of-affected-objects"></a>受影響物件的選取專案  
在視窗左側的 [Sybase 物件樹狀結構] 中，檢查資料表和外鍵的變更，其中應比較是否相同。  
  
如果 SSMA 測試人員無法驗證任何這些物件，您會在 [物件] 樹狀目錄底下看到標示為 [**某些選取的物件**] 的連結包含錯誤。 按一下此連結可查看無法比較這些物件的原因，以及清除錯誤物件的選取專案。  
  
## <a name="table"></a>Table  
[資料表] 索引標籤包含所選資料表的方格視圖。 方格包含下列有關所選資料表的資訊：  
  
-   資料行名稱  
  
-   資料類型  
  
-   Precision  
  
-   調整  
  
-   規則  
  
-   預設  
  
-   身分識別  
  
-   Nullable  
  
## <a name="sql"></a>Sql  
[SQL] 索引標籤包含所選資料表的「建立資料表」 SQL。  
  
## <a name="data"></a>資料  
[資料] 索引標籤會顯示所選資料表中的資料。  
  
## <a name="properties"></a>屬性  
屬性] 索引標籤會顯示選取之資料表的屬性。 下欄欄位會出現在 [屬性] 索引標籤底下：  
  
-   建立或上次修改時間  
  
-   物件名稱  
  
## <a name="table-comparison-settings"></a>資料表比較設定  
在 [**資料表比較**] 頁面上建立 [資料表的比較規則]。 您可以進行下列設定。  
  
### <a name="comparison-mode"></a>比較模式  
定義將在其上執行比較的資料表內容。  
  
-   如果您只選取 [**變更**]，將會執行資料表資料列的完整比較。  
  
-   如果您選取 [**完整**]，則只會執行已變更之資料列的比較。  
  
## <a name="column-comparison-settings"></a>資料行比較設定  
在 [資料**行比較**] 頁面上，建立資料表資料行的比較規則。 您可以進行下列設定。  
  
### <a name="use-during-test-comparisons"></a>在測試比較期間使用  
判斷此資料行是否會參與測試結果驗證。  
  
-   如果您選擇 [ **True**]，SSMA 會在對 Sybase 執行測試之後，使用 SQL Server 中的資料行內容來比較此資料行的內容。
  
-   如果您選擇 [ **False**]，則會從結果驗證中排除資料行。  
  
### <a name="use-custom-scale"></a>使用自訂規模  
對於數值資料類型的資料行，您可以設定比較的自訂小數位數。  
  
-   如果您選擇 [ **True**]，則會在比較之前，根據**比較小**數位數值來進位數值。  
  
-   如果您選擇 [ **False**]，數值比較將會是精確的。  
  
### <a name="comparing-scale"></a>比較尺規  
  
-   只有在 [**使用自訂調整**] 選項設定為 [ **True**] 時才可使用。 這是數值比較的有效位數。  
  
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
  
-   如果您選擇 [ **False**]，則比較將會考慮字母大小寫。  
  
## <a name="comparing-sql"></a>比較 SQL  
您可以在 [**比較 SQL** ] 頁面上，查看 SSMA 測試人員所產生的 SELECT 語句。 測試人員會以逐列方式比較這些語句的結果集。 Sybase 結果集的每個下一個資料列都應該等於中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所產生之結果集的下一個資料列。  
  
您可以編輯這些 SELECT 語句來提供自訂驗證。 若要在 Sybase 和語句中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]儲存變更，請相對地使用來源和目標 SQL 底下的 [套用] 按鈕。 **Apply**  
  
## <a name="next-step"></a>後續步驟  
[自訂呼叫順序 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[&#40;SybaseToSQL&#41;執行測試案例](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;測試遷移的資料庫物件](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
