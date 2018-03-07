---
title: "@@TEXTSIZE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TEXTSIZE'
- '@@TEXTSIZE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, TEXTSIZE option
- SELECT statement [SQL Server], text size returned
- TEXTSIZE option
- '@@TEXTSIZE function'
- text size returned [SQL Server]
ms.assetid: 4308a7b9-8e8f-49e9-8246-8224e32f4953
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38f8444a2b078335b4f1bcfce89da966c55b04dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40textsize-transact-sql"></a>&#x40;&#x40;TEXTSIZE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前的值[TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md)選項。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@TEXTSIZE  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="examples"></a>範例  
 下列範例會使用`SELECT`顯示`@@TEXTSIZE`值之前和之後變更`SET``TEXTSIZE`陳述式。  
  
```  
-- Set the TEXTSIZE option to the default size of 4096 bytes.  
SET TEXTSIZE 0  
SELECT @@TEXTSIZE AS 'Text Size'  
SET TEXTSIZE 2048  
SELECT @@TEXTSIZE AS 'Text Size'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Text Size
-----------
4096
Text Size
-----------
2048
 ```  
  
## <a name="see-also"></a>請參閱＜  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET TEXTSIZE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)  
  
  
