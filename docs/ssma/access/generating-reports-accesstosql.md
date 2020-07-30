---
title: 產生報表（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c9569675fa94b04602b10d0c781fb213fcb307c8
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394820"
---
# <a name="generating-reports-accesstosql"></a>產生報表（AccessToSQL）
在物件樹狀結構層級的 SSMA 主控台中，會產生使用命令執行之特定活動的報告。  
  
使用下列程式來產生報告：  
  
1.  指定**寫入摘要-報告至**參數。 相關的報表會儲存為檔案名（如果有指定）或在您指定的資料夾中。 檔案名依下表所述，是系統預先定義的名稱， ** &lt; n &gt; **是唯一的檔案編號，每次執行相同的命令時，都會以數位遞增。  
  
    報告 vis-à-vis 命令包括：  
  
    |Sl. 不可以。|Command|報表標題|  
    |-|-|-|  
    |1|產生-評量-報告|AssessmentReport &lt; n &gt; 。STL|  
    |2|轉換-架構|SchemaConversionReport &lt; n &gt; 。STL|  
    |3|遷移-資料|DataMigrationReport &lt; n &gt; 。STL|  
    |4|同步處理-目標|TargetSynchronizationReport &lt; n &gt; 。STL|  
    |5|從資料庫重新整理|SourceDBRefreshReport &lt; n &gt; 。STL|  
  
    > [!IMPORTANT]  
    > 輸出報告與評量報告不同。 前者是已執行命令的效能報告，後者則是以程式設計方式取用的 XML 報表。  
  
    適用于輸出報告的命令選項（從 Sl）。 不可以。 2-4），請參閱[執行 SSMA 主控台 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)一節。  
  
2.  使用報表詳細資訊設定，指出您想要在輸出報告中的詳細程度：  
  
    |Sl. 不可以。|命令和參數|輸出描述|  
    |-|-|-|  
    |1|verbose = "false"|產生活動的摘要報告。|  
    |2|verbose = "true"|產生每個活動的摘要和詳細狀態報表。|  
  
    > [!NOTE]  
    > 上述指定的報表詳細資訊設定適用于產生-評估-報告、轉換架構、遷移資料命令。  
  
3.  使用錯誤報表設定，指出您想要在錯誤報表中的詳細程度：  
  
    |Sl. 不可以。|命令和參數|輸出描述|  
    |-|-|-|  
    |1|報告-錯誤 = "false"|錯誤/警告/資訊訊息沒有詳細資料。|  
    |2|報告-錯誤 = "true"|詳細的錯誤/警告/資訊訊息。|  
  
    > [!NOTE]  
    > 上述指定的錯誤報表設定適用于 [產生-評估-報告]、[轉換架構]、[遷移-資料] 命令。  
  
**範例︰**  
  
```xml  
<generate-assessment-report  
  
    object-name="testschema"  
  
    object-type="Schemas"  
  
    verbose="yes"  
  
    report-erors="yes"  
  
    write-summary-report-to="$AssessmentFolder$\Report1.xml"  
  
    assessment-report-folder="$AssessmentFolder$\assesment_report"  
  
    assessment-report-overwrite="true"  
  
/>  
```  
  
### <a name="synchronize-target"></a>同步處理-目標：  
「**同步處理-目標**」命令的「**報告-錯誤**」參數，可指定同步處理作業的錯誤報表位置。 然後，依名稱**TargetSynchronizationReport n 的 &lt; 檔案 &gt; 。XML**會在指定的位置建立，其中** &lt; n &gt; **是唯一的檔案編號，每次執行相同的命令時，都會以數位遞增。  
  
**注意：** 如果指定了資料夾路徑，則 [回報錯誤-到] 參數會變成「同步處理-目標」命令的選擇性屬性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**物件-名稱：** 指定要進行同步處理的物件（也可以有個別物件名稱或群組物件名稱）。  
  
**錯誤：** 指定是否要將同步處理錯誤指定為警告或錯誤。 發生錯誤的可用選項：  
  
-   報告--as 警告  
  
-   報告-每個警告  
  
-   fail-腳本  
  
### <a name="refresh-from-database"></a>從資料庫重新整理：  
[**從資料庫**重新整理] 具有 [回報**錯誤-到**] 參數，可指定重新整理作業的錯誤報表位置。 然後，依名稱**SourceDBRefreshReport n 的 &lt; 檔案 &gt; 。XML**會在指定的位置建立，其中** &lt; n &gt; **是唯一的檔案編號，每次執行相同的命令時，都會以數位遞增。  
  
**注意：** 如果指定了資料夾路徑，則 [回報錯誤-到] 參數會變成「同步處理-目標」命令的選擇性屬性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**物件-名稱：** 指定要重新整理的物件（也可以有個別物件名稱或群組物件名稱）。  
  
**錯誤：** 指定是否將重新整理錯誤指定為警告或錯誤。 發生錯誤的可用選項：  
  
-   報告--as 警告  
  
-   報告-每個警告  
  
-   fail-腳本  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台（存取）](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
