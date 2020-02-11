---
title: XML 輸入檔參考 (Database Engine Tuning Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b560b36eb98ec73723a4ce25cb3c647f4962b634
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62509980"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>XML 輸入檔參考 (Database Engine Tuning Advisor)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]微調 Advisor 可以使用 XML 輸入檔來微調資料庫。 這個 XML 檔會指定微調工作階段要使用哪些資料庫、資料表、工作負載檔或資料表，以及微調選項。 您也可以利用這個檔案來指定使用者指定的組態，以執行「假設」分析。  
  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 輸入檔包含 XML 元素的階層，每個元素都包含指定微調工作階段設定的文字或其他元素。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 輸入檔必須符合格式正確之 XML 的標準，因此，所有元素名稱都會區分大小寫。 元素利用 Pascal 案例來指定，這表示第一個字元是大寫，任何後續串連單字的第一個字母也是大寫。  
  
 所有元素值都必須符合 XML 命名慣例。 如需有關這些慣例的詳細資訊，請參閱 MSDN Library 中的＜ [XML Textual Content](https://go.microsoft.com/fwlink/?LinkId=7614) ＞。  
  
 請注意，這份參考並不完整。 如需有關可用來定義 XML 輸入之所有元素的資訊，請參閱＜ [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor XML 結構描述 (DTASchema.xsd)＞。  
  
## <a name="xml-declaration"></a>XML 宣告  
  
-   [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>DTAXML 根元素  
  
-   [&#40;DTA&#41;的 DTAXML 元素](dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>DTAInput 元素  
  
-   [&#40;DTA&#41;的 DTAInput 元素](dtainput-element-dta.md)  
  
-   [Server 元素 &#40;DTA&#41;](server-element-dta.md)  
  
-   [&#40;DTA&#41;的工作負載元素](workload-element-dta.md)  
  
-   [&#40;DTA&#41;的 TuningOptions 元素](tuningoptions-element-dta.md)  
  
-   [&#40;DTA&#41;的 Configuration 元素](configuration-element-dta.md)  
  
## <a name="server-elements"></a>伺服器元素  
  
-   [Server &#40;DTA&#41;的 Name 元素](name-element-for-server-dta.md)  
  
-   [Server &#40;DTA&#41;的 Database 元素](database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>工作負載元素  
  
-   [&#40;DTA&#41;的 File 元素](file-element-dta.md)  
  
-   [&#40;DTA&#41;的工作負載的 Database 元素](database-element-for-workload-dta.md)  
  
-   [&#40;DTA&#41;的 EventString 元素](eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>微調選項元素  
  
-   [&#40;DTA&#41;的 TuningTimeInMin 元素](tuningtimeinmin-element-dta.md)  
  
-   [&#40;DTA&#41;的 StorageBoundInMB 元素](storageboundinmb-element-dta.md)  
  
-   [&#40;DTA&#41;的 TestServer 元素](testserver-element-dta.md)  
  
-   [&#40;DTA&#41;的 FeatureSet 元素](featureset-element-dta.md)  
  
-   [&#40;DTA&#41;的資料分割元素](partitioning-element-dta.md)  
  
-   [&#40;DTA&#41;的 DropOnlyMode 元素](droponlymode-element-dta.md)  
  
-   [&#40;DTA&#41;的 KeepExisting 元素](keepexisting-element-dta.md)  
  
-   [&#40;DTA&#41;的 OnlineIndexOperation 元素](onlineindexoperation-element-dta.md)  
  
-   [&#40;DTA&#41;的 DatabaseToConnect 元素](databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>組態元素  
  
-   [Configuration &#40;DTA&#41;的 Server 元素](server-element-for-configuration-dta.md)  
  
-   [Configuration &#40;DTA&#41;的 Database 元素](database-element-for-configuration-dta.md)  
  
-   [&#40;DTA&#41;的建議元素](recommendation-element-dta.md)  
  
-   [&#40;DTA&#41;建立元素](create-element-dta.md)  
  
-   [&#40;DTA&#41;的 Index 元素](index-element-dta.md)  
  
-   [&#40;DTA&#41;的索引名稱元素](name-element-for-index-dta.md)  
  
-   [&#40;DTA&#41;之索引的資料行元素](column-element-for-index-dta.md)  
  
-   [資料行 &#40;DTA&#41;的 Name 元素](name-element-for-column-dta.md)  
  
-   [&#40;DTA&#41;的索引的 Filegroup 元素](filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>資料庫元素  
  
-   [資料庫的 Name 元素 &#40;DTA&#41;](name-element-for-database-dta.md)  
  
-   [資料庫的 Schema 元素 &#40;DTA&#41;](schema-element-for-database-dta.md)  
  
-   [&#40;DTA&#41;架構的 Name 元素](name-element-for-schema-dta.md)  
  
-   [用於架構 &#40;DTA&#41;的 Table 元素](table-element-for-schema-dta.md)  
  
-   [資料表 &#40;DTA&#41;的 Name 元素](name-element-for-table-dta.md)  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
