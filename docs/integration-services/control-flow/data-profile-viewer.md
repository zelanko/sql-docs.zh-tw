---
description: 資料設定檔檢視器
title: 資料設定檔檢視器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2ee5f6f01a098c2e8a67b09e915a947010d5758
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484612"
---
# <a name="data-profile-viewer"></a>資料設定檔檢視器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  檢視和分析資料設定檔是資料分析程序中的下一個步驟。 您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝內部執行「資料分析」工作並計算資料設定檔後，檢視這些設定檔。 如需如何設定和執行「資料分析」工作的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。  
  
> [!IMPORTANT]  
>  輸出檔可能包含您資料庫的相關敏感性資料，以及資料庫所包含的資料。 如需如何讓這個檔案更安全的相關建議，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
## <a name="data-profiles"></a>資料設定檔  
 若要檢視資料設定檔，您可以設定「資料分析」工作，將其輸出傳送到檔案，然後使用獨立的「資料設定檔檢視器」即可。 若要開啟資料設定檔檢視器，請執行下列其中一項操作。  
  
-   以滑鼠右鍵按一下 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的 [資料分析] 工作，然後按一下 [編輯]。 在 [資料分析工作編輯器] 的 [一般] 頁面上按一下 [開啟設定檔檢視器]。  
  
-   在 *\<drive>* :\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn 資料夾中，執行 DataProfileViewer.exe。  
  
 此檢視器可使用多個窗格，顯示您所要求與計算之結果的設定檔以及選擇性的詳細資料與向下鑽研能力：  
  
 **設定檔** 窗格  
 [設定檔]  窗格會顯示「資料設定檔」工作所要求的設定檔。 若要檢視設定檔的計算結果，請在 [設定檔]  窗格中選取設定檔，結果就會顯示在檢視器的其他窗格中。  
  
 **結果** 窗格  
 [結果]  窗格會使用單一資料列來摘要說明設定檔的計算結果。 例如，如果您要求 [資料行長度散發設定檔]  ，這個資料列會包含最小和最大長度，以及資料列計數。 對於大部分的設定檔，您可以在 [結果]  窗格中選取這個資料列，以便在選用的 [詳細資料]  窗格中查看其他詳細資料。  
  
 **詳細資料** 窗格  
 對於大部分的設定檔類型，[詳細資料]  窗格會顯示在 [結果]  窗格中選取之設定檔結果的其他相關資訊。 例如，如果您要求 [資料行長度散發設定檔]  ，[詳細資料]  窗格會顯示所找到的每個資料行長度。 此窗格也會顯示資料行值中，具有該資料行長度之資料列的數目與百分比。  
  
 對於根據一個以上的資料行所計算的三種設定檔類型 ([候選索引鍵]、[功能相依性] 與 [值包含])，[詳細資料]  窗格會顯示預期關聯性的違規。 例如，如果您要求 [候選索引鍵設定檔]，[詳細資料] 窗格會顯示違反候選索引鍵唯一性的重複值。  
  
 如果可以使用計算設定檔所使用的資料來源，您可以在 [詳細資料]  窗格中按兩下資料列，以便在 [向下鑽研]  窗格中查看相符的資料列。  
  
 **向下鑽研** 窗格  
 當以下條件成立時，您可以在 [詳細資料]  窗格中按兩下資料列，在 [向下鑽研]  窗格中查看相符的資料列：  
  
-   可以使用用來計算設定檔的資料來源。  
  
-   您具有檢視資料的權限。  
  
 為了連接到來源資料庫完成向下鑽研要求，資料設定檔檢視器會使用 Windows 驗證及目前使用者的認證。 資料設定檔檢視器不會使用儲存在執行「資料分析」工作之封裝內的連接資訊。  
  
> [!IMPORTANT]  
>  資料設定檔檢視器所提供的向下鑽研功能會傳送即時查詢給原始資料來源。 這些查詢對於伺服器的效能可能會有負面影響。  
>   
>  如果您從不是最近建立的輸出檔向下切入，則向下鑽研查詢傳回的資料列集可能與計算原始輸出的資料列集不同。  
  
 如需資料設定檔檢視器之使用者介面的詳細資訊，請參閱 [資料設定檔檢視器 F1 說明](../../integration-services/control-flow/data-profile-viewer-f1-help.md)。  
  
## <a name="data-profile-viewer-f1-help"></a>資料設定檔檢視器 F1 說明
  您可以使用資料設定檔檢視器來檢視資料分析工作的輸出。  
  
 如需如何使用資料設定檔檢視器的詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。 如需如何使用資料分析工作 (建立您在資料設定檔檢視器中分析的設定檔輸出) 的詳細資訊，請參閱 [資料分析工作的設定](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)。  
  
### <a name="static-options"></a>靜態選項  
 **開啟**  
 按一下即可瀏覽包含資料分析工作之輸出的已儲存檔案。  
  
 **設定檔** 窗格  
 展開 [設定檔]  窗格中的樹狀結構，即可查看輸出中所包含的設定檔。 選取設定檔，即可檢視該設定檔的結果。  
  
 **訊息** 窗格  
 顯示狀態訊息。  
  
 **向下鑽研** 窗格  
 顯示符合輸出中某個值的資料列 (如果資料分析工作所使用的資料來源可用的話)。  
  
 例如，如果您要針對「美國州名」資料行檢視資料行值散發設定檔的輸出， **[詳細值散發]** 窗格可能會包含 "WA" 的資料列。 在 [詳細值散發]  窗格中按兩下該資料列，即可利用 [向下鑽研] 窗格查看 [州] 資料行值為 "WA" 的資料列。  
  
### <a name="dynamic-options"></a>動態選項  
  
#### <a name="profile-type--column-length-distribution-profile"></a>設定檔類型 = 資料行長度散發設定檔  
  
##### <a name="column-length-distribution-profile---column-pane"></a>資料行長度散發設定檔 - \<column> 窗格  
 **最小長度**  
 顯示這個資料行中值的最小長度。  
  
 **最大長度**  
 顯示這個資料行中值的最大長度。  
  
 **忽略開頭空白**  
 顯示這個設定檔會以 **IgnoreLeadingSpaces** 值為 True 或 False 的情況進行計算。 這個屬性是在 [資料分析工作編輯器] 的 **[設定檔要求]** 頁面上設定的。  
  
 **忽略尾端空白**  
 顯示這個設定檔會以 **IgnoreLeadingSpaces** 值為 True 或 False 的情況進行計算。 這個屬性是在 [資料分析工作編輯器] 的 **[設定檔要求]** 頁面上設定的。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
##### <a name="detailed-length-distribution-pane"></a>詳細長度散發窗格  
 **長度**  
 顯示在已分析資料行中找到的資料行長度。  
  
 **Count**  
 顯示已分析資料行的值具有 [長度]  資料行中所顯示之長度的資料列數目。  
  
 **百分比**  
 顯示已分析資料行的值具有 [長度]  資料行中所顯示之長度的資料列百分比。  
  
#### <a name="profile-type--column-null-ratio-profile"></a>設定檔類型 = 資料行 Null 比例設定檔  
  
##### <a name="column-null-ratio-profile---column-pane"></a>資料行 Null 比例設定檔 - \<column> 窗格  
 **Null 計數**  
 顯示已分析資料行具有 Null 值的資料列數目。  
  
 **Null 百分比**  
 顯示已分析資料行具有 Null 值的資料列百分比。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
#### <a name="profile-type--column-pattern-profile"></a>設定檔類型 = 資料行模式設定檔  
  
##### <a name="column-pattern-profile---column-pane"></a>資料行模式設定檔 - \<column> 窗格  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
##### <a name="pattern-distribution-pane"></a>模式散發窗格  
 **模式**  
 顯示針對已分析資料行所計算的模式。  
  
 **百分比**  
 顯示值符合 [模式]  資料行中所顯示之模式的資料列百分比。  
  
#### <a name="profile-type--column-statistics-profile"></a>設定檔類型 = 資料行統計資料設定檔  
  
##### <a name="column-statistics-profile---column-pane"></a>資料行統計資料設定檔 - \<column> 窗格  
 **最低**  
 顯示在已分析資料行中找到的最小值。  
  
 **最大值**  
 顯示在已分析資料行中找到的最大值。  
  
 **平均數**  
 顯示在已分析資料行中找到之值的平均數。  
  
 **標準差**  
 顯示在已分析資料行中找到之值的標準差。  
  
#### <a name="profile-type--column-value-distribution-profile"></a>設定檔類型 = 資料行值散發設定檔  
  
##### <a name="column-value-distribution-profile---column-pane"></a>資料行值散發設定檔 - \<column> 窗格  
 **相異值的數目**  
 顯示在已分析資料行中找到之相異值的計數。  
  
 **資料列計數**  
 顯示資料表或檢視表中的資料列數目。  
  
##### <a name="detailed-value-distribution-pane"></a>詳細值散發窗格  
 **ReplTest1**  
 顯示在已分析資料行中找到的相異值。  
  
 **Count**  
 顯示已分析資料行具有 [值]  資料行中所顯示之值的資料列數目。  
  
 **百分比**  
 顯示已分析資料行具有 [值]  資料行中所顯示之值的資料列百分比。  
  
#### <a name="profile-type--candidate-key-profile"></a>設定檔類型 = 候選索引鍵設定檔  
  
##### <a name="candidate-key-profile---table-pane"></a>候選索引鍵設定檔 - \<table> 窗格  
 **索引鍵資料行**  
 顯示針對分析成候選索引鍵所選取的資料行。  
  
 **索引鍵強度**  
 顯示候選索引鍵資料行或資料行組合的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示存在重複的值。  
  
##### <a name="key-violations-pane"></a>索引鍵違規窗格  
 **\<column1>、\<column2> 等。**  
 顯示在已分析資料行中找到的重複值。  
  
 **Count**  
 顯示指定之資料行具有第一個資料行中所顯示之值的資料列數目。  
  
#### <a name="profile-type--functional-dependency-profile"></a>設定檔類型 = 功能相依性設定檔  
  
##### <a name="functional-dependency-profile-pane"></a>功能相依性設定檔窗格  
 **[行列式資料行]**  
 顯示選取成為行列式資料行的資料行。 在相同美國郵遞區號應該永遠具有相同州名的範例中，郵遞區號就是行列式資料行。  
  
 **相依資料行**  
 顯示選取成為相依資料行的資料行。 在相同美國郵遞區號應該永遠具有相同州名的範例中，州名就是相依資料行。  
  
 **功能相依性強度**  
 顯示資料行之間功能相依性的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示發生了行列式值無法決定相依值的情況。 在相同美國郵遞區號應該永遠具有相同州名的範例中，這可能表示某些州名的值無效。  
  
##### <a name="functional-dependency-violations-pane"></a>功能相依性違規窗格  
  
> [!NOTE]  
>  如果資料中錯誤值的百分比很高，可能會導致功能相依性設定檔產生非預期的結果。 例如，在 90% 的資料列中，州值 "WI" 代表郵遞區號值 "98052"。 此設定檔會將包含正確州值 "WA" 的資料列回報成違規。  
  
 **\<determinant column name>**  
 顯示這個功能相依性違規的執行個體中行列式資料行或資料行組合的值。  
  
 **\<dependent column name>**  
 顯示這個功能相依性違規的執行個體中相依資料行的值。  
  
 **支持度計數**  
 顯示行列式資料行值會決定相依資料行的資料列數目。  
  
 **違規計數**  
 顯示行列式資料行值無法決定相依資料行的資料列數目 (這些是相依值為 **\<dependent column name>** 資料行中顯示值的資料列。)  
  
 **支持度百分比**  
 顯示行列式資料行會決定相依資料行的資料列百分比。  
  
#### <a name="profile-type--value-inclusion-profile"></a>設定檔類型 = 值包含設定檔  
  
##### <a name="value-inclusion-profile-pane"></a>值包含設定檔窗格  
 **[子集資料行]**  
 顯示經過分析以便判斷是否位於超集資料行中的資料行或資料行組合。  
  
 **[超集資料行]**  
 顯示經過分析以便判斷是否包含子集資料行中之值的資料行或資料行組合。  
  
 **包含強度**  
 顯示資料行之間重疊的強度 (以百分比為單位)。 小於 100% 的索引鍵強度表示發生了在超集值中找不到子集值的情況。  
  
##### <a name="inclusion-violations-pane"></a>包含違規窗格  
 **\<column1>、\<column2> 等。**  
 顯示子集資料行中的值，但這些值在超集資料行中找不到。  
  
 **Count**  
 顯示指定之資料行具有第一個資料行中所顯示之值的資料列數目。  
  
