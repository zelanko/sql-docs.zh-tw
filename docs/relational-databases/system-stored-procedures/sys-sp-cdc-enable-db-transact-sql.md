---
title: sys.databases sp_cdc_enable_db （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9a7a07452a0dcb9ebfe91e7e51b10239b3eb3f15
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769636"
---
# <a name="syssp_cdc_enable_db-transact-sql"></a>sys.sp_cdc_enable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  啟用目前資料庫的異動資料擷取。 您必須先針對資料庫執行這個程序，然後才能針對該資料庫中的任何資料表啟用異動資料擷取。 異動資料擷取會記錄套用至已啟用資料表的插入、更新和刪除活動，並以方便取用的關聯式格式提供變更的詳細資料。 系統會針對修改的資料列擷取鏡像追蹤來源資料表之資料行結構的資料行資訊，以及將變更套用至目標環境所需的中繼資料。  
  
> [!IMPORTANT]
>  並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 無法在[系統資料庫](../../relational-databases/databases/system-databases.md)或散發資料庫上啟用變更資料捕獲。  
  
 sys.sp_cdc_enable_db 會建立具有整個資料庫範圍的異動資料擷取物件，包括中繼資料資料表和 DDL 觸發程序。 它也會建立 cdc 架構和 cdc 資料庫使用者，並將[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視中資料庫專案的 is_cdc_enabled 資料行設定為1。  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會啟用異動資料擷取。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_disable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
