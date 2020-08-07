---
title: 使用範例主控台腳本檔案 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Sample Console Script Files
ms.assetid: ef221118-b442-4ca6-9409-6ee1d9f8d948
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7db44b317ee91044748519b93c7cdc175c96a94d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934467"
---
# <a name="working-with-the-sample-console-script-files-sybasetosql"></a>使用範例主控台指令碼檔 (SybaseToSQL)
已提供一些範例檔案以及使用者參考和使用方式的產品。 本節說明可輕鬆自訂這些腳本以符合使用者需求的方式。  
  
## <a name="sample-console-script-files"></a>範例主控台腳本檔案  
下列範例主控台腳本檔案已針對使用者參考提供涵蓋的不同案例：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml：**  
  
    -   這個範例會為來源和目標資料庫提供不同的連線模式，而使用者可以依據需求選取任何模式。 這個範例包含伺服器定義。  
  
    -   只要將值變更為所需的來源和目標伺服器定義，使用者就可以連接到所需的資料庫。 在提供的範例中，所有值都已提供為可在**VariableValueFileSample.xml**中使用的變數值。  所有其他連接參數可以從使用者的工作伺服器連接檔案中移除。  
  
    -   如需連接到來源和目標伺服器的詳細資訊，請參閱[&#40;SybaseToSQL&#41;建立伺服器連接](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)檔案。  
  
-   **VariableValueFileSample.xml：**  
    已在範例主控台腳本檔案中使用，且已在此檔案中自動分頁的所有變數 `ServersConnectionFileSample.xml` 。 若要執行範例主控台腳本，使用者必須使用使用者定義的值來取代範例變數值，並將此檔案當做額外的命令列引數，連同腳本檔案一起傳遞。  
  
    如需變數值檔案的詳細資訊，請參閱[&#40;SybaseToSQL&#41;建立變數值](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)檔案。  
  
-   **AssessmentReportGenerationSample.xml：**  
    這個範例可讓使用者在開始轉換和遷移資料之前，產生可供使用者用來進行分析的 xml 評估報告。  
  
    在 `generate-assessment-report` 命令中，使用者必須 mandatorily 變更變數值 (將屬性中**VariableValueFileSample.xml**) 參考 `object-name` 到使用者正在使用的資料庫名稱。 視指定的物件類型而定，此 `object-type` 值也必須一併變更。  
  
    如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `generate-assessment-report` 範例主控台指令檔的範例4所示。  
  
    如需產生報表的詳細資訊，請參閱[&#40;SybaseToSQL&#41;產生報表](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
    > [!NOTE]  
    > -   請確定將變數值檔案命令列引數傳遞至主控台應用程式，並以使用者指定的值更新 VariableValueFileSample.xml。  
    > -   請確定伺服器連接檔案命令列引數已傳遞至主控台應用程式，而且已使用正確的伺服器參數值來更新 ServersConnectionFileSample.xml。  
  
-   **SqlStatementConversionSample.xml：**  
    這個範例可讓使用者 `t-sql` 針對 `sql` 提供做為輸入的源資料庫命令，產生對應的腳本。  
  
    在 `convert-sql-statement` 使用者必須 mandatorily 變更變數值的命令中， (將屬性中**VariableValueFileSample.xml**) 參考 `context` 到使用者正在使用的資料庫名稱。 使用者也必須將 `sql` 屬性值變更為其需要轉換的源資料庫 `sql` 命令。  
  
    使用者也可以提供要轉換的 sql 檔案。 範例主控台腳本檔案的範例4中已說明這 `convert-sql-statement` 種情況。  
  
    > [!NOTE]  
    > 請確定將變數值檔案命令列引數傳遞至主控台應用程式，並以使用者指定的值更新 VariableValueFileSample.xml。  
  
-   **ConversionAndDataMigrationSample.xml：**  
     這個範例可讓使用者執行端對端遷移，使其無法轉換為資料移轉。 如下所示，需要變更的必要屬性值清單如下：  
  
    **命令名稱**  
  
    `map-schema`  
  
    源資料庫與目標架構的架構對應。  
  
    **屬性**  
  
    -   `source-schema:`指定需要轉換的源資料庫。  
  
    -   `sql-server-schema`：指定要遷移至的目標資料庫  
  
    **命令名稱**  
  
    `convert-schema`  
  
    -   執行從來源到目標架構的架構轉換。  
  
    -   如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `convert-schema` 範例主控台指令檔的範例4所示。  
  
    **屬性**  
  
    `object-name`：指定需要轉換的源資料庫/物件名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`  
  
    **命令名稱**  
  
    `synchronize-target`  
  
    -   同步處理目標物件與目標資料庫。  
  
    -   如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `synchronize-target` 範例主控台指令檔的範例3所示。  
  
    **屬性**  
  
    `object-name:`指定需要建立的 sql server 資料庫/物件名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`  
  
    **命令名稱**  
  
    `migrate-data`  
  
    -   將源資料移轉至目標。  
  
    -   如果使用者必須評估多個物件/資料庫，他可以指定多個 `metabase-object` 節點，如 `migrate-data` 範例主控台指令檔的範例2中所示。  
  
    **屬性**  
  
    `object-name:`指定需要遷移的源資料庫/資料表名稱。 確定對應的 `object-type` 已根據指定的物件類型而變更。`object-name`  
  
## <a name="see-also"></a>另請參閱  
[建立變數值檔案 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
[&#40;SybaseToSQL 建立伺服器連接檔案&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
[&#40;SybaseToSQL&#41;產生報表](../../ssma/sybase/generating-reports-sybasetosql.md)  
  
