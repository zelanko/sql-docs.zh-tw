---
description: '使用範例主控台指令檔 (DB2ToSQL) '
title: 使用範例主控台指令檔 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5c3080c3-d074-4f99-a5f5-219ebeddc474
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d609900151e7ced05be4cc92e65c06270b6ef8a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426920"
---
# <a name="working-with-the-sample-console-script-files-db2tosql"></a>使用範例主控台指令檔 (DB2ToSQL) 
提供一些範例檔案，以及使用者參考和使用方式的產品。 本節說明可輕鬆自訂這些腳本以符合使用者需求的方式。  
  
## <a name="sample-console-script-files"></a>範例主控台指令檔  
下列範例主控台腳本檔案已提供給使用者參考，其中涵蓋不同的案例：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
1.  **ServersConnectionFileSample.xml：**  
  
    -   這個範例會提供來源和目標資料庫可用的不同連接模式，使用者可以根據需求選取任何模式。 此範例包含伺服器定義。  
  
    -   使用者只要將值變更為所需的來源和目標伺服器定義，就可以連接到所需的資料庫。 在提供的範例中，所有值都是以 **VariableValueFileSample.xml**提供的變數值提供。  您可以從使用者的工作伺服器連接檔案中移除所有其他連接參數。  
  
    -   如需有關連接到來源和目標伺服器的詳細資訊，請參閱 [建立伺服器連接檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md) 。  
  
2.  **VariableValueFileSample.xml：** 在範例主控台指令檔中使用的所有變數，都已 `ServersConnectionFileSample.xml` 在這個檔案中進行定序。 若要執行範例主控台腳本，使用者必須直接以使用者定義的值取代範例變數值，並將此檔案作為額外的命令列引數一起傳遞給腳本檔案。  
  
    如需變數值檔案的詳細資訊，請參閱 [建立變數值檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)。  
  
3.  **AssessmentReportGenerationSample.xml：** 此範例可讓使用者產生 xml 評量報告，讓使用者在開始轉換和遷移資料之前，可供使用者用來進行分析。  
  
    在 `generate-assessment-report` 使用者必須與變更變數值的命令中 (將屬性中的 **VariableValueFileSample.xml**) 參考 `object-name` 到使用者正在使用的資料庫名稱。 視指定的物件類型而定， `object-type` 值也必須變更。  
  
    如果使用者必須評估多個物件/資料庫，則可以指定多個 `metabase-object` 節點，如 `generate-assessment-report` 範例主控台腳本檔案的範例4命令所示。  
  
    如需有關產生報表的詳細資訊，請參閱 [&#40;DB2ToSQL&#41;產生報表 ](../../ssma/db2/generating-reports-db2tosql.md)。  
  
    **注意：**  
  
    確定變數值檔案命令列引數已傳遞至主控台應用程式，且 VariableValueFileSample.xml 會以使用者指定的值更新。  
  
    確定已將伺服器連接檔案命令列引數傳遞到主控台應用程式，並以正確的伺服器參數值更新 ServersConnectionFileSample.xml。  
  
4.  **SqlStatementConversionSample.xml：** 這個範例可讓使用者 `t-sql` 針對以輸入形式提供的源資料庫命令，產生對應的腳本 `sql` 。  
  
    在 `convert-sql-statement` 使用者必須與變更變數值的命令中 (將屬性中的 **VariableValueFileSample.xml**) 參考 `context` 到使用者正在使用的資料庫名稱。 使用者也必須將 `sql` 屬性值變更為 `sql` 需要轉換之源資料庫命令的值。  
  
    使用者也可以提供要轉換的 sql 檔案。 這已在 `convert-sql-statement` 範例主控台指令檔的命令範例4中說明。  
  
    > [!NOTE]  
    > 確定變數值檔案命令列引數已傳遞至主控台應用程式，且 VariableValueFileSample.xml 會以使用者指定的值更新。  
  
5.  **ConversionAndDataMigrationSample.xml：** 此範例可讓使用者執行端對端遷移，從轉換到資料移轉。 以下列出需要變更的強制屬性值清單：  
  
    |命令名稱：|描述|屬性|  
    |----------------|---------------|-------------|  
    |`map-schema`|源資料庫與目標架構的架構對應。|`source-schema:` 指定需要轉換的源資料庫。<br /><br />`sql-server-schema`：指定要遷移至的目標資料庫|  
    |`convert-schema`|執行從來源到目標架構的架構轉換。<br /><br />如果使用者必須評估多個物件/資料庫，則可以指定多個 `metabase-object` 節點，如 `convert-schema` 範例主控台腳本檔案的範例4命令所示。|`object-name`：指定需要轉換的源資料庫/物件名稱。 確定對應的 `object-type` 會根據在中指定的物件類型而變更。 `object-name`|  
    |`synchronize-target`|將目標物件與目標資料庫進行同步處理。<br /><br />如果使用者必須評估多個物件/資料庫，則可以指定多個 `metabase-object` 節點，如 `synchronize-target` 範例主控台腳本檔中命令的範例3所示。|`object-name:` 指定需要建立的 sql server 資料庫/物件名稱。 確定對應的 `object-type` 會根據在中指定的物件類型而變更。 `object-name`|  
    |`migrate-data`|將源資料移轉至目標。<br /><br />如果使用者必須評估多個物件/資料庫，則可以指定多個 `metabase-object` 節點，如 `migrate-data` 範例主控台腳本檔的範例2所示。|`object-name:` 指定需要遷移的源資料庫/資料表名稱。 確定對應的 `object-type` 會根據在中指定的物件類型而變更。 `object-name`|  
  
## <a name="see-also"></a>另請參閱  
[建立變數值檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
[建立伺服器連接檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
[&#40;DB2ToSQL&#41;產生報表 ](../../ssma/db2/generating-reports-db2tosql.md)  
  
