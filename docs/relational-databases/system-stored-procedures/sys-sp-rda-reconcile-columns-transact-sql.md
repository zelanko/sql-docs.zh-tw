---
title: "sys.sp_rda_reconcile_columns (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bae454caa630025bb4470dc69da7fa4a97f6307
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  協調遠端 Azure 資料表中的資料行中的資料行已啟用 Stretch 的 SQL Server 資料表。  
    
  **sp_rda_reconcile_columns**將資料行加入遠端資料表存在於已啟用 Stretch 的 SQL Server 資料表中，但不是在遠端資料表。 這些資料行可能會不小心刪除遠端資料表中的資料行。 不過， **sp_rda_reconcile_columns**不會從遠端資料表存在於遠端資料表中，但不是在 SQL Server 資料表中刪除資料行。
  
  > [!IMPORTANT]
  > 當 **sp_rda_reconcile_columns** 重新建立您不小心從遠端資料表中刪除的資料行時，它不會還原先前存在於已刪除資料行中的資料。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>引數  
 @objname = '*@objname*'  
 已啟用 Stretch 的 SQL Server 資料表的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  
   
## <a name="remarks"></a>備註  
 如果遠端 Azure 資料表中有些資料行已不再存在於已啟用延展功能的 SQL Server 資料表中，這些額外的資料行並不會影響 Stretch Database 的正常運作。 您也可以手動移除額外的資料行。  
  
## <a name="example"></a>範例  
 若要先協調的遠端 Azure 資料表中的資料行執行下列陳述式。  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
