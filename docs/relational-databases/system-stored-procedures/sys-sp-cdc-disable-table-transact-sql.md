---
title: sys.sp_cdc_disable_table & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b797301b5b778bea34ad1552152e7e3e147dde37
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169168"
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前資料庫中指定的來源資料表和擷取執行個體，停用異動資料擷取。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@source_schema=** ] **'**_來源\_結構描述_**'**  
 這是容納來源資料表的結構描述名稱。 *source_schema&lt*已**sysname**，沒有預設值，不能是 NULL。  
  
 *source_schema&lt*必須存在於目前的資料庫。  
  
 [  **@source_name=** ] **'**_來源\_名稱_**'**  
 這是要停用異動資料擷取的來源資料表名稱。 *source_name*已**sysname**，沒有預設值，不能是 NULL。  
  
 *source_name*必須存在於目前的資料庫。  
  
 [  **@capture_instance=** ] **'**_擷取\_執行個體_**'** | **'** 所有 **'**  
 這是要針對指定之來源資料表停用的擷取執行個體名稱。 *capture_instance*已**sysname**不能是 NULL。  
  
 指定 'all' 時，所有擷取執行個體定義*source_name*會停用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sys.sp_cdc_disable_table**異動資料擷取變更資料表和系統函數指定的來源資料表和擷取執行個體相關聯的卸除。 它會刪除指定的擷取執行個體的異動資料擷取系統資料表並將設定從相關聯的任何資料列**is_tracked_by_cdc**資料行中的資料表項目[sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)目錄檢視設為 0。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會停用 `HumanResources.Employee` 資料表的異動資料擷取。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_enable_table &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
