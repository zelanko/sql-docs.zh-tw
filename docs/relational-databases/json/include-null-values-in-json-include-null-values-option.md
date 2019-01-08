---
title: 在 JSON 中包含 Null 值 - INCLUDE_NULL_VALUES 選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 264fb99c4bda933fdb5acfbcfe2674e36eecbe4c
ms.sourcegitcommit: 0330cbd1490b63e88334a9f9e421f4bd31a6083f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2018
ms.locfileid: "52886696"
---
# <a name="include-null-values-in-json---includenullvalues-option"></a>在 JSON 中包含 Null 值 - INCLUDE_NULL_VALUES 選項
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  若要在 **FOR JSON** 子句的 JSON 輸出中包含 Null 值，請指定 **INCLUDE_NULL_VALUES** 選項。  
  
 如果不指定 **INCLUDE_NULL_VALUES** 選項，JSON 輸出就不會包含查詢結果中的 Null 值屬性。  
  
## <a name="examples"></a>範例  
 下列範例顯示使用或不使用 **INCLUDE_NULL_VALUES** 選項的 **FOR JSON** 子句輸出。  
  
|不使用 **INCLUDE_NULL_VALUES** 選項|使用 **INCLUDE_NULL_VALUES** 選項|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 以下是使用 **INCLUDE_NULL_VALUES** 選項之 **FOR JSON** 子句的另一個範例。  
  
 **[資料集屬性]**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **結果**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
