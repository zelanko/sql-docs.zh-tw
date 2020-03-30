---
title: XML 輸入檔參考
titleSuffix: Database Engine Tuning Advisor
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 12646cd7f2c737696f8c86d25c9c6bf2d6c2ada8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247514"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 輸入檔參考 (Database Engine Tuning Advisor)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 可以利用 XML 輸入檔來微調資料庫。 這個 XML 檔會指定微調工作階段要使用哪些資料庫、資料表、工作負載檔或資料表，以及微調選項。 您也可以利用這個檔案來指定使用者指定的組態，以執行「假設」分析。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 輸入檔包含 XML 元素的階層，每個元素都包含指定微調工作階段設定的文字或其他元素。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 輸入檔必須符合格式正確之 XML 的標準，因此，所有元素名稱都會區分大小寫。 元素利用 Pascal 案例來指定，這表示第一個字元是大寫，任何後續串連單字的第一個字母也是大寫。  
  
 所有元素值都必須符合 XML 命名慣例。 如需有關這些慣例的詳細資訊，請參閱 MSDN Library 中的＜ [XML Textual Content](https://go.microsoft.com/fwlink/?LinkId=7614) ＞。  
  
 請注意，這份參考並不完整。 如需有關可用來定義 XML 輸入之所有元素的資訊，請參閱＜ [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 結構描述 (DTASchema.xsd)＞。  
  
## <a name="xml-declaration"></a>XML 宣告  
  
-   [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML 根元素  
  
-   [DTAXML 元素 &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 元素  
  
-   [DTAInput 元素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload 元素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)  
  
-   [TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Configuration 元素 &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>伺服器元素  
  
-   [伺服器的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [伺服器的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>工作負載元素  
  
-   [File 元素 &#40;DTA&#41;](../../tools/dta/file-element-dta.md)  
  
-   [工作負載的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [EventString 元素 &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>微調選項元素  
  
-   [TuningTimeInMin 元素 &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [StorageBoundInMB 元素 &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [TestServer 元素 &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet 元素 &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning 元素 &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode 元素 &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting 元素 &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation 元素 &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [DatabaseToConnect 元素 &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>組態元素  
  
-   [組態的 Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [組態的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Recommendation 元素 &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Create 元素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index 元素 &#40;DTA&#41;](../../tools/dta/index-element-dta.md)  
  
-   [索引的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [索引的 Column 元素 &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [資料行的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [索引的 Filegroup 元素 &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>資料庫元素  
  
-   [資料庫的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [資料庫的 Schema 元素 &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [結構描述的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [結構描述的 Table 元素 &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [資料表的 Name 元素 &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
