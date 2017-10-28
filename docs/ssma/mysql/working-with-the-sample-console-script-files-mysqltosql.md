---
title: "使用範例主控台指令碼檔案 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sample console script files
ms.assetid: 7e6aaa8a-5f5c-414d-9fb8-21e56b9ffaef
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 84a1bddb2cb42011d5150257e5dd28ebab1a9ade
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-the-sample-console-script-files-mysqltosql"></a>使用範例主控台指令碼檔案 (MySQLToSQL)
幾個範例檔案與產品一起提供給使用者參考和使用方式。 本章節描述的方式，輕鬆地自訂這些指令碼，以符合使用者需求。  
  
## <a name="sample-console-script-files"></a>範例主控台指令碼檔案  
下列範例主控台指令碼檔案涵蓋不同的案例提供給使用者參考：  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   這個範例可讓來源和目標資料庫的連線使用不同的模式，且使用者可以選擇根據需求的任何模式。 此範例包含的伺服器定義。  
  
    -   使用者可以連接到所需的資料庫，只要變更所需的來源和目標伺服器定義的值。 所提供的範例中的所有值已都提供為變數的值中可用的**VariableValueFileSample.xml**。  可以從使用者的工作伺服器的連接檔案中移除所有其他連接參數。  
  
    -   如需有關如何連接到來源和目標伺服器的詳細資訊，請參閱[建立伺服器連接檔案 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) .  
  
-   **VariableValueFileSample.xml:**已經用於範例主控台的所有變數指令都碼檔案和`ServersConnectionFileSample.xml`有這個檔案中已定序。 若要執行使用者具有取代範例變數的範例主控台指令碼值與使用者定義的並將此檔案傳遞做為其他命令列引數，以及指令碼檔案。  
  
    如需有關變數的值檔案的詳細資訊，請參閱[建立變數值的檔案 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md).  
  
-   **AssessmentReportGenerationSample.xml:**此範例可讓使用者產生的 xml 評估報表可由使用者進行分析他開始轉換並移轉資料之前。  
  
    在`generate-assessment-report`命令 mandatorily 變更變數的值，使用者必須 (請參閱**VariableValueFileSample.xml**) 中`object-name`屬性加入資料庫名稱會出現在使用者使用。 根據指定的物件類型`object-type`值也必須變更。  
  
    如果使用者以評估多個物件具有 / 資料庫他可以指定多個`metabase-object`節點中所示`generate-assessment-report`命令的範例 4 的範例主控台指令碼檔案。  
  
    如需有關如何產生報告的詳細資訊，請參閱[產生報表 &#40;MySQLToSQL &#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
    **注意：**  
  
    -   請確認變數值檔命令列引數會傳遞給主控台應用程式，然後 VariableValueFileSample.xml 會更新為指定的使用者值。  
  
    -   請確認伺服器連線檔命令列引數會傳遞給主控台應用程式，然後 ServersConnectionFileSample.xml 的正確的伺服器參數值來更新。  
  
-   **SqlStatementConversionSample.xml:**  
    這個範例可讓使用者以產生對應`t-sql`來源資料庫的指令碼`sql`提供做為輸入的命令。  
  
    中`convert-sql-statement`命令，使用者必須 mandatorily 變更變數的值 (請參閱**VariableValueFileSample.xml**) 中`context`屬性設定為要由使用者所使用的資料庫名稱。 使用者也必須變更`sql`屬性值的來源資料庫`sql`最初轉換所需的命令。  
  
    使用者也可以提供要轉換的 sql 檔案。 這已在說明`convert-sql-statement`命令的範例 4 的範例主控台指令碼檔案。  
  
    > [!NOTE]  
    > 請確認變數值檔命令列引數會傳遞給主控台應用程式，然後 VariableValueFileSample.xml 會更新為指定的使用者值。  
  
-   **ConversionAndDataMigrationSample.xml:**  
     這個範例可讓使用者從資料移轉至轉換執行端對端移轉。 強制屬性值，它們將會需要變更清單如下：  
  
    **命令名稱**  
  
    `map-schema`  
  
    目標結構描述的來源資料庫的結構描述對應。  
  
    **屬性**  
  
    -   `source-schema:`指定轉換所需的來源資料庫。  
  
    -   `sql-server-schema`： 指定要移轉到目標資料庫  
  
    **命令名稱**  
  
    `convert-schema`  
  
    1.  執行從來源到目標結構描述的結構描述轉換。  
  
    2.  如果使用者以評估多個物件具有 / 資料庫他可以指定多個`metabase-object`節點中所示`convert-schema`命令的範例 4 的範例主控台指令碼檔案。  
  
    **屬性**  
  
    `object-name`： 指定來源資料庫/將物件轉換所需的名稱。 請確認對應`object-type`會依據物件中指定的類型變更`object-name`  
  
    **命令名稱**  
  
    `synchronize-target`  
  
    1.  目標物件會同步處理目標資料庫。  
  
    2.  如果使用者以評估多個物件具有 / 資料庫他可以指定多個`metabase-object`節點中所示`synchronize-target`命令的範例主控台指令碼檔案的範例 3。  
  
    **屬性**  
  
    `object-name:`指定 sql server 資料庫/物件建立所需的名稱。 請確認對應`object-type`會依據物件中指定的類型變更`object-name`  
  
    **命令名稱**  
  
    `migrate-data`  
  
    1.  將來源資料移轉到目標。  
  
    2.  如果使用者以評估多個物件具有 / 資料庫他可以指定多個`metabase-object`節點中所示`migrate-data`命令的範例 2 的範例主控台指令碼檔案。  
  
    **屬性**  
  
    `object-name:`指定來源資料庫/資料表移轉所需的名稱。 請確認對應`object-type`會依據物件中指定的類型變更`object-name`  
  
## <a name="see-also"></a>另請參閱  
[建立變數值的檔案 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
[建立伺服器連接檔案 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
[產生報表 &#40;MySQLToSQL &#41;](../../ssma/mysql/generating-reports-mysqltosql.md)  
  

