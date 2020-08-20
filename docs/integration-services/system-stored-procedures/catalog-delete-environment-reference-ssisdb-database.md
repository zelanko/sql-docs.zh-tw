---
description: catalog.delete_environment_reference (SSISDB 資料庫)
title: catalog.delete_environment_reference (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1f68f157-c4e9-412c-92b3-53a2faaba29b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5ec190a40b71b874d2b888adff31ad99a41db1f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456915"
---
# <a name="catalogdelete_environment_reference-ssisdb-database"></a>catalog.delete_environment_reference (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案刪除環境參考。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.delete_environment_reference [ @reference_id = ] reference_id  
```  
  
## <a name="arguments"></a>引數  
 [ @reference_id = ] *reference_id*  
 環境參考的唯一識別碼。 *reference_id* 是 **bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   環境參考識別碼無效  
  
-   使用者未具備適當的權限  
  
  
