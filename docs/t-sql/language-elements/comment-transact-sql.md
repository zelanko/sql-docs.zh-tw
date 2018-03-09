---
title: "-（註解） (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2cae636f23fc166246b3cf6cb755fde570b3d19c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="---comment-transact-sql"></a>-- (註解) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指出使用者提供的文字。 註解可以插入個別行中、以巢狀方式放在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令列尾端，或放在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式內。 伺服器不會評估註解。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>引數  
 *text_of_comment*  
 這是包含註解文字的字元字串。  
  
## <a name="remarks"></a>備註  
 單行註解或巢狀註解使用兩個連字號 (--)。 新行字元會終止利用 -- 插入的註解。 註解沒有長度上限。 下表列出您可以用來註解或取消註解文字的鍵盤快速鍵。  
  
|動作|Standard|  
|------------|--------------|  
|讓所選的文字變成註解|CTRL+K、CTRL+C|  
|將所選的文字取消註解|CTRL+K、CTRL+U|  
  
 如需鍵盤快速鍵的詳細資訊，請參閱[SQL Server Management Studio 鍵盤快速鍵](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)。  
  
 對於多行註解，請參閱[斜線星狀 &#40;區塊註解 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>範例  
 下列範例會使用 -- 註解化字元。  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [流程控制語言 (TRANSACT-SQL)](~/t-sql/language-elements/control-of-flow.md)  
  
  
