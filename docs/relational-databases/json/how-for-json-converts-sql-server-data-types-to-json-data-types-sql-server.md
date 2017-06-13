---
title: "FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 527cb99c5caf0bb805e17f3b77b7d5e017e28ace
ms.contentlocale: zh-tw
ms.lasthandoff: 06/09/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 子句使用下列規則，在 JSON 輸出中將 SQL Server 資料類型轉換為 JSON 類型。  
  
|類別目錄|SQL Server 資料類型|JSON 資料類型|  
|--------------|--------------|---------------|  
|字元和字串類型|char、 nchar、 varchar、 nvarchar|string|  
|數值類型|int、bigint、float、decimal、numeric|number|  
|位元類型|bit|布林值 (true 或 false)|  
|日期和時間類型|date、datetime、datetime2、time、datetimeoffset|string|  
|二進位類型|varbinary、binary、image、timestamp、rowversion|BASE64 編碼字串|  
|CLR 類型|geometry、 geography、 其他 CLR 類型|不支援。 這些類型傳回錯誤。<br /><br /> 在 SELECT 陳述式中，使用 CAST 或 CONVERT，或使用 CLR 屬性或方法，將來源資料轉換成可以成功地轉換成 JSON 類型的 SQL Server 資料類型。 例如，使用**stastext （)** geometry 類型使用，或使用**tostring （)**針對任何 CLR 類型。 JSON 輸出值的型別然後衍生自您在 SELECT 陳述式中套用轉換的傳回型別。|  
|其他類型|uniqueidentifier、money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

