---
title: catalog.delete_environment_reference (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1f68f157-c4e9-412c-92b3-53a2faaba29b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 37dc6d2623a2efbdf566bdc71f9a5b1c7f33724a
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274694"
---
# <a name="catalogdeleteenvironmentreference-ssisdb-database"></a>catalog.delete_environment_reference (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案刪除環境參考。  
  
## <a name="syntax"></a>語法  
  
```sql  
delete_environment_reference [ @reference_id = ] reference_id  
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
  
  
