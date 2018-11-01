---
title: PolyBase 功能和限制 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2052b098f0be7ab377cf38a36b896794d3caa07a
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874346"
---
# <a name="polybase-features-and-limitations"></a>PolyBase 功能和限制

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

適用於 SQL Server 產品和服務的 PolyBase 功能摘要。  
  
## <a name="feature-summary-for-product-releases"></a>產品版本的功能摘要

本表會摘要說明 PolyBase 的重要功能以及提供這些功能的產品。  
  
||||||
|-|-|-|-|-|   
|**功能**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL 資料倉儲**|**平行處理資料倉儲**| 
|使用下列項目查詢 Hadoop 資料： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|否|否|是|
|從 Hadoop 匯入資料|是|否|否|是|
|匯出資料至 Hadoop  |是|否|否| 是|
|在 HDInsights 中查詢、匯入、匯出 |否|否|否|否
|將查詢計算下推到 Hadoop|是|否|否|是|  
|從 Azure Blob 儲存體匯入資料|是|否|是|是| 
|匯出資料至 Azure Blob 儲存體|是|否|是|是|  
|從 Azure Data Lake Store 匯入資料|否|否|是|否|    
|從 Azure Data Lake Store 匯出資料|否|否|是|否|
|從 Microsoft 的 BI 工具執行 PolyBase 查詢|是|否|是|是|   

## <a name="pushdown-computation-supported-t-sql-operators"></a>支援計算下推的 T-SQL 運算子

在 SQL Server 和 APS 中，並非所有 T-SQL 運算子都可以下推到 Hadoop 叢集。 下表列出所有支援的運算子和部分不受支援的運算子。 

||||
|-|-|-| 
|**運算子類型**|**可推送到 Hadoop**|**可推送到 Blob 儲存體**|
|資料行投影|是|否|
|述詞|是|否|
|彙總|部分|否|
|外部資料表之間的聯結|否|否|
|外部資料表和本機資料表之間的聯結|否|否|
|排序|否|否|

部分彙總表示最後的彙總必須在資料到達 SQL Server 時立即進行，但是一部分的彙總會在 Hadoop 中進行。 這是大量平行處理系統計算彙總的常見方法。  

## <a name="known-limitations"></a>已知限制

PolyBase 具有下列限制：

- 在 SQL Server 中最大資料列大小 (包括變數長度資料行的完整長度) 不能超過 32 KB，在 Azure SQL 資料倉儲中則不能超過 1 MB。

- PolyBase 不支援 Hive 0.12 以上的資料類型 (也就是 Char()、VarChar())

- 將資料從 SQL Server 或 Azure SQL 資料倉儲匯出為 ORC 檔案格式時，可以將具有大量文字的資料行限制為最少 50 個資料行，因為會發生 Java 記憶體不足錯誤。 若要解決這個問題，只需要匯出資料行的子集。

- 無法讀取或寫入在 Hadoop 中靜止加密的資料， 包括 HDFS 加密區域或透明加密。

- 如果已啟用 KNOX，PolyBase 就無法連接至 Hortonworks 執行個體。

- 若您使用 Hive 資料表，且 transactional = true，PolyBase 就無法存取 Hive 資料表目錄中的資料。

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [將節點新增至 SQL Server 2016 容錯移轉叢集時，不會安裝 PolyBase](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

::: moniker-end
- 不支援整合式驗證。 目前只支援使用者名稱和密碼。  
- 我們預設會啟用加密。 若要停用加密，您必須...
- [類型對應限制](polybase-type-mapping.md)


## <a name="security-and-authentication"></a>安全性和驗證 

## <a name="see-also"></a>另請參閱  

[PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
