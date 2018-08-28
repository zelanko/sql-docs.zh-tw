---
title: PolyBase 建立版本的功能摘要 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc95156f93b6b87d317348f56e1b06f57439ada2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102106"
---
# <a name="polybase-versioned-feature-summary"></a>PolyBase 建立版本的功能摘要
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
## <a name="see-also"></a>另請參閱  
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  
