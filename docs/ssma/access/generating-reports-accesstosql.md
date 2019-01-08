---
title: 產生報表 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fe6f45b2e35761fac5f8c49012b1eb370645bcb1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52412765"
---
# <a name="generating-reports-accesstosql"></a>產生報表 (AccessToSQL)
使用命令來執行某些活動的報表會產生物件樹狀結構層級的 SSMA 主控台中。  
  
您可以使用下列程序來產生報表：  
  
1.  指定**寫入-摘要-報表-以**參數。 （如果有指定），將會儲存為檔案名稱的相關的報表，或在您指定的資料夾中。 檔案名稱是系統預先定義的位置，如下表所述**&lt;n&gt;** 是唯一的檔案數目，以每次執行相同的命令數字會遞增。  
  
    報表 vis-相對-vis 命令如下：  
  
    ||||  
    |-|-|-|  
    |**Sl。[否]。**|**Command**|**報表標題**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|移轉資料|DataMigrationReport&lt;n&gt;。XML|  
    |4|同步處理目標|TargetSynchronizationReport&lt;n&gt;.XML|  
    |5|從資料庫重新整理|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > 輸出報表與不同評定報告。 前者是一種報表執行的命令時的效能，後者是以程式設計方式使用的 XML 報表。  
  
    如需命令選項，輸出報告 （從 Sl。 資料分割 上述的 2-4)，請參閱[執行 SSMA 主控台&#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md)一節。  
  
2.  表示您想要輸出報表使用報表的詳細資訊設定的詳細資料程度：  
  
    ||||  
    |-|-|-|  
    |**Sl。[否]。**|**命令與參數**|**輸出描述**|  
    |1|詳細資訊 ="false"|產生之活動的摘要的報告。|  
    |2|詳細資訊 ="true"|產生每個活動的摘要和詳細狀態報告。|  
  
    > [!NOTE]  
    > 上面指定的報表詳細等級設定時產生評估報表、 轉換結構描述移轉資料的命令。  
  
3.  表示您想要在錯誤報表中使用錯誤報告設定的詳細資料程度：  
  
    ||||  
    |-|-|-|  
    |**Sl。[否]。**|**命令與參數**|**輸出描述**|  
    |1|報告錯誤 ="false"|沒有詳細資料發生錯誤 / 警告 / 資訊訊息。|  
    |2|報告錯誤 ="true"|詳細的錯誤 / 警告 / 資訊訊息。|  
  
    > [!NOTE]  
    > 錯誤報告設定上述指定時產生評估報表、 轉換結構描述移轉資料的命令。  
  
**範例：**  
  
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
  
### <a name="synchronize-target"></a>同步處理目標：  
命令**同步處理目標**已**報告錯誤至**參數，指定同步處理作業的錯誤報表的位置。 然後，依名稱的檔案**TargetSynchronizationReport&lt;n&gt;。XML**會建立在指定的位置，其中**&lt;n&gt;** 是唯一的檔案數目，以每次執行相同的命令數字會遞增。  
  
**注意：** 如果指定的資料夾路徑，則 '報表-錯誤-to' 參數會變成命令' 同步處理目標 ' 的選擇性屬性。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**物件名稱：** 指定視為 （它也可以有個別的物件名稱或群組的物件名稱） 的同步處理的物件。  
  
**錯誤：** 指定是否要指定同步處理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
-   報表-總計-為-警告  
  
-   報表-每個-為-警告  
  
-   失敗指令碼  
  
### <a name="refresh-from-database"></a>重新整理從-資料庫：  
命令**從資料庫重新整理**已**報告錯誤至**參數，指定重新整理作業的錯誤報表的位置。 然後，依名稱的檔案**SourceDBRefreshReport&lt;n&gt;。XML**會建立在指定的位置，其中**&lt;n&gt;** 是唯一的檔案數目，以每次執行相同的命令數字會遞增。  
  
**注意：** 如果指定的資料夾路徑，則 '報表-錯誤-to' 參數會變成命令' 同步處理目標 ' 的選擇性屬性。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**物件名稱：** 指定重新整理 （它也可以有個別的物件名稱或群組的物件名稱） 被視為物件。  
  
**錯誤：** 指定是否要指定重新整理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
-   報表-總計-為-警告  
  
-   報表-每個-為-警告  
  
-   失敗指令碼  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 （存取）](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
