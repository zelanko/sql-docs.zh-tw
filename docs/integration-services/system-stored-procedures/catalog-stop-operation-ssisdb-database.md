---
title: catalog.stop_operation (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7747cf7087006460b5e2dc2d79c7c0e403436c42
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的驗證或執行執行個體。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>引數  
 [ @operation_id = ] *operation_id*  
 驗證或執行執行個體的唯一識別碼。 *operation_id* 是 **bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   驗證或執行執行個體的 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   作業識別碼無效  
  
-   作業已停止  
  
## <a name="remarks"></a>Remarks  
 一次只能有一個使用者停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的作業。 如果多個使用者嘗試停止作業，預存程序將會在第一次嘗試時傳回成功 (值 `0`)，但後續的嘗試將會引發錯誤。  
  
  
