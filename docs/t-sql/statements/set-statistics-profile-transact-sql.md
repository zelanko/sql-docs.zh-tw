---
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6494f792c1dcfbb92bfe48d3063df533d0ff1510
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  顯示陳述式的設定檔資訊。 STATISTICS PROFILE 適用於隨選查詢、檢視和預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 當 STATISTICS PROFILE 是 ON 時，每個執行的查詢都會傳回它的正規結果集，後面再接著顯示查詢執行設定檔的其他結果集。  
  
 其他結果集包含查詢的 SHOWPLAN_ALL 資料行及這些其他資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**資料列**|每個運算子所產生的實際資料列數|  
|**Executes**|運算子已執行的次數|  
  
## <a name="permissions"></a>Permissions  
 若要使用 SET STATISTICS PROFILE 和檢視輸出，使用者必須有下列許可權：  
  
-   執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的適當許可權。  
  
-   包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所參考的物件之所有資料庫的 SHOWPLAN 權限。  
  
 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式不會產生 STATISTICS PROFILE 結果集，就只需要執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的適當權限。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會產生 STATISTICS PROFILE 結果集，檢查 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式執行權限和 SHOWPLAN 權限都必須成功，否則，便會中止執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，且不會產生任何顯示計畫資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
