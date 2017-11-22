---
title: "FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d934c3ddaee2d87a0a4afa5f9df900f759a1ed7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 子句使用下列規則，在 JSON 輸出中將 SQL Server 資料類型轉換為 JSON 類型。  
  
|類別目錄|SQL Server 資料類型|JSON 資料類型|  
|--------------|--------------|---------------|  
|字元和字串類型|char、nchar、varchar、nvarchar|string|  
|數值類型|int、bigint、float、decimal、numeric|number|  
|位元類型|bit|布林值 (true 或 false)|  
|日期和時間類型|date、datetime、datetime2、time、datetimeoffset|string|  
|二進位類型|varbinary、binary、image、timestamp、rowversion|BASE64 編碼字串|  
|CLR 類型|geometry、geography、 他 CLR 類型|不支援。 這些類型傳回錯誤。<br /><br /> 在 SELECT 陳述式中，使用 CAST 或 CONVERT，或使用 CLR 屬性或方法，將來源資料轉換成可以順利轉換成 JSON 類型的 SQL Server 資料類型。 例如，針對幾何類型使用 **STAsText()**，或針對任何 CLR 類型使用 **ToString()**。 之後 JSON 輸出值的類型會衍生自您在 SELECT 陳述式中套用的轉換傳回類型。|  
|其他類型|uniqueidentifier、money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解 SQL Server 中的內建 JSON 支援  
對於大量的特定解決方案、使用案例和建議，請參閱 SQL Server 和 Azure SQL Database 中 Microsoft 經理專案 Jovan Popovic 所撰寫的[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
