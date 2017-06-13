---
title: "在 JSON 中包含 Null 值 - INCLUDE_NULL_VALUES 選項 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 2cdb047169569041e3a8f7890d8215fd87284959
ms.contentlocale: zh-tw
ms.lasthandoff: 06/09/2017

---
# <a name="include-null-values-in-json---includenullvalues-option"></a>在 JSON 中包含 Null 值 - INCLUDE_NULL_VALUES 選項
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要在 **FOR JSON** 子句的 JSON 輸出中包含 Null 值，請指定 **INCLUDE_NULL_VALUES** 選項。  
  
 如果不指定 **INCLUDE_NULL_VALUES** 選項，JSON 輸出就不會包含查詢結果中的 Null 值屬性。  
  
## <a name="examples"></a>範例  
 下列範例顯示使用或不使用 **INCLUDE_NULL_VALUES** 選項的 **FOR JSON** 子句輸出。  
  
|不使用 **INCLUDE_NULL_VALUES** 選項|使用 **INCLUDE_NULL_VALUES** 選項|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 以下是使用 **INCLUDE_NULL_VALUES** 選項之 **FOR JSON** 子句的另一個範例。  
  
 **查詢**  
  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。  

## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

