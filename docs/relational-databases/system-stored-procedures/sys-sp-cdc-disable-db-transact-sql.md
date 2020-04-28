---
title: sys.databases sp_cdc_disable_db （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: f8d85103b48b04284966e77595d0cfa927cd6338
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083757"
---
# <a name="syssp_cdc_disable_db-transact-sql"></a>sys.sp_cdc_disable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停用目前資料庫的異動資料擷取。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
**適用**于： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至[目前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
sys.sp_cdc_disable_db  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_cdc_disable_db**會停用目前已啟用資料庫中所有資料表的變更資料捕獲。 與異動資料擷取相關的所有系統物件 (例如，變更資料表、作業、預存程序和函數) 都會一併卸除。 [Sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視中資料庫專案的 [ **is_cdc_enabled** ] 資料行設定為0。  
  
> [!NOTE]  
>  如果停用異動資料擷取時，針對資料庫定義了許多擷取執行個體，長時間執行的交易可能會導致 sys.sp_cdc_disable_db 的執行失敗。 您可以在執行 sys.sp_cdc_disable_db 之前，使用 sys.sp_cdc_disable_table 來停用個別的擷取執行個體，藉以避免這個問題。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會停用 `AdventureWorks2012` 資料庫的異動資料擷取。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_db;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_enable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)   
 [sp_cdc_disable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)  
  
  
