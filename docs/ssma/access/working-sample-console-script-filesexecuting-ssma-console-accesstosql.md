---
title: 使用範例主控台腳本 FilesExecuting SSMA 主控台 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e18677df3b1997c994e940cf41930771f7a1cd38
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937452"
---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>使用範例主控台腳本 FilesExecuting SSMA 主控台 (AccessToSQL) 
已提供一些範例檔案以及使用者參考和使用方式的產品。 本節說明可輕鬆自訂這些腳本以符合使用者需求的方式。  
  
## <a name="sample-console-script-files"></a>範例主控台腳本檔案  
下列範例主控台腳本檔案已針對使用者參考提供涵蓋的不同案例：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml：**  
  
    -   這個範例會為來源和目標資料庫提供不同的連線模式，而使用者可以依據需求選取任何模式。 這個範例包含伺服器定義。  
  
    -   只要將值變更為所需的來源和目標伺服器定義，使用者就可以連接到所需的資料庫。 在提供的範例中，所有值都已提供為可在**VariableValueFileSample.xml**中使用的變數值。 所有其他連接參數可以從使用者的工作伺服器連接檔案中移除。  
  
    -   如需連接到來源和目標伺服器的詳細資訊，請參閱[&#40;AccessToSQL&#41;建立伺服器連接](../../ssma/access/creating-the-server-connection-files-accesstosql.md)檔案。  
  
-   **VariableValueFileSample.xml：** 已在範例主控台腳本檔案中使用，且已在此檔案中自動分頁的所有變數 `ServersConnectionFileSample.xml` 。 若要執行範例主控台腳本，使用者必須使用使用者定義的值來取代範例變數值，並將此檔案當做額外的命令列引數，連同腳本檔案一起傳遞。  
  
    如需變數值檔案的詳細資訊，請參閱[&#40;AccessToSQL&#41;建立變數值](../../ssma/access/creating-variable-value-files-accesstosql.md)檔案。  
  
-   **AssessmentReportGenerationSample.xml：** 這個範例可讓使用者在開始轉換和遷移資料之前，產生可供使用者用來進行分析的 xml 評估報告。  
  
    在 `generate-assessment-report` 命令中，使用者必須 mandatorily 變更變數值 (將屬性中**VariableValueFileSample.xml**) 參考 `object-name` 到使用者正在使用的資料庫名稱。 視指定的物件類型而定，此 `object-type` 值也必須一併變更。  
  
    如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `generate-assessment-report` 範例主控台指令檔的範例4所示。  
  
    如需產生報表的詳細資訊，請參閱[&#40;AccessToSQL&#41;產生報表](../../ssma/access/generating-reports-accesstosql.md)。  
  
    > [!NOTE]  
    > -   請確定將變數值檔案命令列引數傳遞至主控台應用程式，並以使用者指定的值更新 VariableValueFileSample.xml。  
    > -   請確定伺服器連接檔案命令列引數已傳遞至主控台應用程式，而且已使用正確的伺服器參數值來更新 ServersConnectionFileSample.xml。  
  
-   **ConversionAndDataMigrationSample.xml：** 這個範例可讓使用者執行端對端遷移，使其無法轉換為資料移轉。 如下所示，需要變更的必要屬性值清單如下：  
  
    |命令名稱：|描述|屬性|  
    |----------------|---------------|-------------|  
    |`map-schema`|源資料庫與目標架構的架構對應。|`source-schema:`指定需要轉換的源資料庫。<br /><br />`sql-server-schema`：指定要遷移至的目標資料庫|  
    |`convert-schema`|執行從來源到目標架構的架構轉換。<br /><br />如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `convert-schema` 範例主控台指令檔的範例4所示。|`object-name`：指定需要轉換的源資料庫/物件名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`|  
    |`synchronize-target`|同步處理目標物件與目標資料庫。<br /><br />如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `synchronize-target` 範例主控台指令檔的範例3所示。|`object-name:`指定需要建立的 sql server 資料庫/物件名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`|  
    |`migrate-data`|將源資料移轉至目標。<br /><br />如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `migrate-data` 範例主控台指令檔的範例2中所示。|`object-name:`指定需要遷移的源資料庫/資料表名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`|  
  
## <a name="see-also"></a>另請參閱  
[建立變數值檔案 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[&#40;AccessToSQL 建立伺服器連接檔案&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[&#40;AccessToSQL&#41;產生報表](../../ssma/access/generating-reports-accesstosql.md)  
  
