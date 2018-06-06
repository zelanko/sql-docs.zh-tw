---
title: SET CONCAT_NULL_YIELDS_NULL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cc4261d54d86300783499871f50b5ec7d7d152fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-concatnullyieldsnull-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制是否將串連結果當作 Null 或空字串值來處理。  
  
> [!IMPORTANT]  
>  在將來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，CONCAT_NULL_YIELDS_NULL 一定會是 ON，而且明確將此選項設定為 OFF 的應用程式將會產生錯誤。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>Remarks  
 當 SET CONCAT_NULL_YIELDS_NULL 是 ON 時，串連 NULL 值和字串會產生 NULL 結果。 例如，`SELECT 'abc' + NULL` 會產生 `NULL`。 當 SET CONCAT_NULL_YIELDS_NULL 是 OFF 時，串連 Null 值和字串會產生字串本身 (將 Null 值當作空字串來處理)。 例如，`SELECT 'abc' + NULL` 會產生 `abc`。  
  
 如果未指定 SET CONCAT_NULL_YIELDS_NULL，則會套用 **CONCAT_NULL_YIELDS_NULL** 資料庫選項的設定。  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL 與 ALTER DATABASE 的 CONCAT_NULL_YIELDS_NULL 設定相同。  
  
 SET CONCAT_NULL_YIELDS_NULL 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 當您建立或變更計算資料行索引或索引檢視時，SET CONCAT_NULL_YIELDS_NULL 必須是 ON。 如果 SET CONCAT_NULL_YIELDS_NULL 是 OFF，任何含計算資料行索引的資料表或索引檢視之 CREATE、UPDATE、INSERT 和 DELETE 陳述式將會失敗。 如需使用索引檢視表和計算資料行索引時所需之 SET 選項設定的詳細資訊，請參閱 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md) 中的＜使用 SET 陳述式時的考量＞一節。  
  
 當 CONCAT_NULL_YIELDS_NULL 設為 OFF 時，無法出現跨越伺服器界限的字串串連。  
  
 若要檢視此設定的目前設定，請執行下列查詢。  
  
```  
DECLARE @CONCAT_NULL_YIELDS_NULL VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_NULL_YIELDS_NULL = 'ON';  
SELECT @CONCAT_NULL_YIELDS_NULL AS CONCAT_NULL_YIELDS_NULL;  
  
```  
  
## <a name="examples"></a>範例  
 下列範例顯示如何使用這兩個 `SET CONCAT_NULL_YIELDS_NULL` 設定。  
  
```  
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
