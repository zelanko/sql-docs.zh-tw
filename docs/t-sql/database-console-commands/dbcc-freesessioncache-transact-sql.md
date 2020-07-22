---
title: DBCC FREESESSIONCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESESSIONCACHE
- FREESESSIONCACHE_TSQL
- DBCC_FREESESSIONCACHE_TSQL
- DBCC FREESESSIONCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC FREESESSIONCACHE statement
- distributed queries [SQL Server], cache
- clearing distributed query cache
- flushing distributed query cache
ms.assetid: a256ba63-7e11-4d5e-abc0-1fa4ed072e63
author: pmasl
ms.author: umajay
ms.openlocfilehash: 30a4245b58b9da0d51a246ba025533f42b17a715
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485247"
---
# <a name="dbcc-freesessioncache-transact-sql"></a>DBCC FREESESSIONCACHE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

排清分散式查詢對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所用的分散式查詢連線快取。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
```sql
DBCC FREESESSIONCACHE [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
下列範例會排清散發的查詢快取。
  
```sql
USE AdventureWorks2012;  
GO  
DBCC FREESESSIONCACHE WITH NO_INFOMSGS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
