---
title: sys.sp_cdc_disable_db & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_disable_db
- sys.sp_cdc_disable_db_TSQL
- sp_cdc_disable_db_TSQL
- sys.sp_cdc_disable_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_db
- sys.sp_cdc_disable_db
- change data capture [SQL Server], disabling databases
ms.assetid: 420fb99e-e60f-445b-b568-da96471f1e8f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9febaf5b21b840e2bc02a17ed3e38828801de3b1
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53200967"
---
# <a name="sysspcdcdisabledb-transact-sql"></a>sys.sp_cdc_disable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停用目前資料庫的異動資料擷取。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[最新版本](https://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
sys.sp_cdc_disable_db  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sys.sp_cdc_disable_db**停用異動資料擷取目前已啟用資料庫中的所有資料表。 與異動資料擷取相關的所有系統物件 (例如，變更資料表、作業、預存程序和函數) 都會一併卸除。 **Is_cdc_enabled**資料行中的資料庫項目[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視會設為 0。  
  
> [!NOTE]  
>  如果停用異動資料擷取時，針對資料庫定義了許多擷取執行個體，長時間執行的交易可能會導致 sys.sp_cdc_disable_db 的執行失敗。 您可以在執行 sys.sp_cdc_disable_db 之前，使用 sys.sp_cdc_disable_table 來停用個別的擷取執行個體，藉以避免這個問題。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會停用 `AdventureWorks2012` 資料庫的異動資料擷取。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_db;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_enable_db &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)   
 [sys.sp_cdc_disable_table &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)  
  
  
