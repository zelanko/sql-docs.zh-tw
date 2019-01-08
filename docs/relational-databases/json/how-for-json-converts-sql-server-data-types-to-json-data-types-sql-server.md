---
title: FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7475254de99fc01f36388a73434bde4e04420394
ms.sourcegitcommit: 0330cbd1490b63e88334a9f9e421f4bd31a6083f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2018
ms.locfileid: "52886733"
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
