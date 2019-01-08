---
title: sys.sp_cdc_enable_db & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9778d44f3a11bcea066aea3ef43d36489b5daded
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211507"
---
# <a name="sysspcdcenabledb-transact-sql"></a>sys.sp_cdc_enable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 無法在啟用異動資料擷取[系統資料庫](../../relational-databases/databases/system-databases.md)或散發資料庫。  
  
 sys.sp_cdc_enable_db 會建立具有整個資料庫範圍的異動資料擷取物件，包括中繼資料資料表和 DDL 觸發程序。 它也會建立 cdc 結構描述和 cdc 資料庫使用者，並設定 is_cdc_enabled 資料行中的資料庫項目[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視，以 1。  
  
## <a name="permissions"></a>Permissions  
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
 [sys.sp_cdc_disable_db &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
