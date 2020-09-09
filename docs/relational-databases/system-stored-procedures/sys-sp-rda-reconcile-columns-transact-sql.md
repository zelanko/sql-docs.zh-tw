---
title: sys. sp_rda_reconcile_columns (Transact-sql) |Microsoft Docs
description: 瞭解 sys. sp_rda_reconcile_columns。 使用這個預存程式來協調遠端 Azure 資料表中的資料行和已啟用 Stretch 的 SQL Server 資料表中的資料行。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1788e373c8bab330182df9338e447946cda87bd3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538439"
---
# <a name="syssp_rda_reconcile_columns-transact-sql"></a>sys. sp_rda_reconcile_columns (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  將遠端 Azure 資料表中的資料行協調成已啟用 Stretch 的 SQL Server 資料表中的資料行。  
    
  **sp_rda_reconcile_columns** 將資料行加入到已啟用 Stretch 的 SQL Server 資料表中，但不在遠端資料表中的遠端資料表。 這些資料行可能是您不小心從遠端資料表中刪除的資料行。 不過， **sp_rda_reconcile_columns** 不會從遠端資料表中刪除存在於遠端資料表中的資料行，而不會刪除 SQL Server 資料表中的資料行。
  
  > [!IMPORTANT]
  > 當 **sp_rda_reconcile_columns** 重新建立您不小心從遠端資料表中刪除的資料行時，它不會還原先前存在於已刪除資料行中的資料。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>引數  
 \@objname = '* \@ objname*'  
 已啟用 Stretch SQL Server 資料表的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)   
  
## <a name="permissions"></a>權限  
 需要 db_owner 許可權。  
   
## <a name="remarks"></a>備註  
 如果遠端 Azure 資料表中有些資料行已不再存在於已啟用延展功能的 SQL Server 資料表中，這些額外的資料行並不會影響 Stretch Database 的正常運作。 您也可以手動移除額外的資料行。  
  
## <a name="example"></a>範例  
 若要調解遠端 Azure 資料表中的資料行，請執行下列語句。  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
