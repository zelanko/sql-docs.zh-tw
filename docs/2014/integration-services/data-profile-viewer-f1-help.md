---
title: 資料設定檔檢視器 F1 說明 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], viewer
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 41f29fae6a9f9284bd35b2779029d7b3f176bcd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030577"
---
# <a name="data-profile-viewer-f1-help"></a>資料設定檔檢視器 F1 說明
  您可以使用資料設定檔檢視器來檢視資料分析工作的輸出。  
  
 如需如何使用資料設定檔檢視器的詳細資訊，請參閱 [資料設定檔檢視器](control-flow/data-profile-viewer.md)。 如需如何使用資料分析工作 (建立您在資料設定檔檢視器中分析的設定檔輸出) 的詳細資訊，請參閱 [資料分析工作的設定](control-flow/data-profiling-task.md)。  
  
## <a name="static-options"></a>靜態選項  
 **開啟**  
 按一下即可瀏覽包含資料分析工作之輸出的已儲存檔案。  
  
 **設定檔** 窗格  
 展開 [設定檔] 窗格中的樹狀結構，即可查看輸出中所包含的設定檔。 選取設定檔，即可檢視該設定檔的結果。  
  
 **訊息** 窗格  
 顯示狀態訊息。  
  
 **向下鑽研** 窗格  
 顯示符合輸出中某個值的資料列 (如果資料分析工作所使用的資料來源可用的話)。  
  
 例如，如果您要針對「美國州名」資料行檢視資料行值散發設定檔的輸出， **[詳細值散發]** 窗格可能會包含 "WA" 的資料列。 在 [詳細值散發] 窗格中按兩下該資料列，即可利用 [向下鑽研] 窗格查看 [州] 資料行值為 "WA" 的資料列。  
  
## <a name="dynamic-options"></a>動態選項  
  
### <a name="profile-type--column-length-distribution-profile"></a>設定檔類型 = 資料行長度散發設定檔  
  
#### <a name="column-length-distribution-profile---column-pane"></a>資料行長度散發設定檔 - \<資料行> 窗格  
 **最小長度**  
 顯示這個資料行中值的最小長度。  
  
 **最大長度**  
 顯示這個資料行中值的最大長度。  
  
 **忽略開頭空白**  
 顯示與所計算出此設定檔是否`IgnoreLeadingSpaces`True 或 False 的值。 這個屬性是在 [資料分析工作編輯器] 的 **[設定檔要求]** 頁面上設定的。  
  
 **忽略尾端空白**  
 顯示與所計算出此設定檔是否`IgnoreTrailingSpaces`True 或 False 的值。 這個屬性是在 [資料分析工作編輯器] 的 **[設定檔要求]** 頁面上設定的。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
#### <a name="detailed-length-distribution-pane"></a>詳細長度散發窗格  
 **長度**  
 顯示在已分析資料行中找到的資料行長度。  
  
 **Count**  
 顯示已分析資料行的值具有 [長度] 資料行中所顯示之長度的資料列數目。  
  
 **百分比**  
 顯示已分析資料行的值具有 [長度] 資料行中所顯示之長度的資料列百分比。  
  
### <a name="profile-type--column-null-ratio-profile"></a>設定檔類型 = 資料行 Null 比例設定檔  
  
#### <a name="column-null-ratio-profile---column-pane"></a>資料行 Null 比例設定檔 - \<資料行> 窗格  
 **Null 計數**  
 顯示已分析資料行具有 Null 值的資料列數目。  
  
 **Null 百分比**  
 顯示已分析資料行具有 Null 值的資料列百分比。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
### <a name="profile-type--column-pattern-profile"></a>設定檔類型 = 資料行模式設定檔  
  
#### <a name="column-pattern-profile---column-pane"></a>資料行模式設定檔 - \<資料行> 窗格  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
#### <a name="pattern-distribution-pane"></a>模式散發窗格  
 **模式**  
 顯示針對已分析資料行所計算的模式。  
  
 **百分比**  
 顯示值符合 [模式] 資料行中所顯示之模式的資料列百分比。  
  
### <a name="profile-type--column-statistics-profile"></a>設定檔類型 = 資料行統計資料設定檔  
  
#### <a name="column-statistics-profile---column-pane"></a>資料行統計資料設定檔 - \<資料行> 窗格  
 **最小值**  
 顯示在已分析資料行中找到的最小值。  
  
 **最大值**  
 顯示在已分析資料行中找到的最大值。  
  
 **平均數**  
 顯示在已分析資料行中找到之值的平均數。  
  
 **標準差**  
 顯示在已分析資料行中找到之值的標準差。  
  
### <a name="profile-type--column-value-distribution-profile"></a>設定檔類型 = 資料行值散發設定檔  
  
#### <a name="column-value-distribution-profile---column-pane"></a>資料行值散發設定檔 - \<資料行> 窗格  
 **相異值的數目**  
 顯示在已分析資料行中找到之相異值的計數。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
#### <a name="detailed-value-distribution-pane"></a>詳細值散發窗格  
 **ReplTest1**  
 顯示在已分析資料行中找到的相異值。  
  
 **Count**  
 顯示已分析資料行具有 [值] 資料行中所顯示之值的資料列數目。  
  
 **百分比**  
 顯示已分析資料行具有 [值] 資料行中所顯示之值的資料列百分比。  
  
### <a name="profile-type--candidate-key-profile"></a>設定檔類型 = 候選索引鍵設定檔  
  
#### <a name="candidate-key-profile---table-pane"></a>候選索引鍵設定檔 - \<資料表> 窗格  
 **索引鍵資料行**  
 顯示針對分析成候選索引鍵所選取的資料行。  
  
 **索引鍵強度**  
 顯示候選索引鍵資料行或資料行組合的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示存在重複的值。  
  
#### <a name="key-violations-pane"></a>索引鍵違規窗格  
 **\<資料行1>、\<資料行2> 等等。**  
 顯示在已分析資料行中找到的重複值。  
  
 **Count**  
 顯示指定之資料行具有第一個資料行中所顯示之值的資料列數目。  
  
### <a name="profile-type--functional-dependency-profile"></a>設定檔類型 = 功能相依性設定檔  
  
#### <a name="functional-dependency-profile-pane"></a>功能相依性設定檔窗格  
 **行列式資料行**  
 顯示選取成為行列式資料行的資料行。 在相同美國郵遞區號應該永遠具有相同州名的範例中，郵遞區號就是行列式資料行。  
  
 **相依資料行**  
 顯示選取成為相依資料行的資料行。 在相同美國郵遞區號應該永遠具有相同州名的範例中，州名就是相依資料行。  
  
 **功能相依性強度**  
 顯示資料行之間功能相依性的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示發生了行列式值無法決定相依值的情況。 在相同美國郵遞區號應該永遠具有相同州名的範例中，這可能表示某些州名的值無效。  
  
#### <a name="functional-dependency-violations-pane"></a>功能相依性違規窗格  
  
> [!NOTE]  
>  如果資料中錯誤值的百分比很高，可能會導致功能相依性設定檔產生非預期的結果。 例如，在 90% 的資料列中，州值 "WI" 代表郵遞區號值 "98052"。 此設定檔會將包含正確州值 "WA" 的資料列回報成違規。  
  
 **\<行列式資料行名稱>**  
 顯示這個功能相依性違規的執行個體中行列式資料行或資料行組合的值。  
  
 **\<相依資料行名稱>**  
 顯示這個功能相依性違規的執行個體中相依資料行的值。  
  
 **支持度計數**  
 顯示行列式資料行值會決定相依資料行的資料列數目。  
  
 **違規計數**  
 顯示行列式資料行值無法決定相依資料行的資料列數目 (這些是相依值為 **\<相依資料行名稱>** 資料行中所顯示之值的資料列)。  
  
 **支持度百分比**  
 顯示行列式資料行會決定相依資料行的資料列百分比。  
  
### <a name="profile-type--value-inclusion-profile"></a>設定檔類型 = 值包含設定檔  
  
#### <a name="value-inclusion-profile-pane"></a>值包含設定檔窗格  
 **子集資料行**  
 顯示經過分析以便判斷是否位於超集資料行中的資料行或資料行組合。  
  
 **超集資料行**  
 顯示經過分析以便判斷是否包含子集資料行中之值的資料行或資料行組合。  
  
 **包含強度**  
 顯示資料行之間重疊的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示發生了在超集值中找不到子集值的情況。  
  
#### <a name="inclusion-violations-pane"></a>包含違規窗格  
 **\<資料行1>、\<資料行2> 等等。**  
 顯示子集資料行中的值，但這些值在超集資料行中找不到。  
  
 **Count**  
 顯示指定之資料行具有第一個資料行中所顯示之值的資料列數目。  
  
## <a name="see-also"></a>另請參閱  
 [資料設定檔檢視器](control-flow/data-profile-viewer.md)   
 [資料分析工作和檢視器](control-flow/data-profiling-task-and-viewer.md)  
  
  