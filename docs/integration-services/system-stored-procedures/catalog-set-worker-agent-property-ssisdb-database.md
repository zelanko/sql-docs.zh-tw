---
title: catalog.set_worker_agent_property (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 121c39ddc217cbdc178ca8ea8221081ce33eee4b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912780"
---
# <a name="catalogset_worker_agent_property-ssisdb-database"></a>catalog.set_worker_agent_property (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的屬性。

## <a name="syntax"></a>語法

```sql
catalog.set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId
    , [ @PropertyName = ] PropertyName
    , [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>引數
[@WorkerAgentId =] *WorkerAgentId*  
Scale Out Worker 的背景工作代理程式識別碼。 *WorkerAgentId* 是 **uniqueidentifier**。

[@PropertyName =] *PropertyName*  
屬性的名稱。 *PropertyName* 是 **nvarchar(256)** 。

[@PropertyValue =] *PropertyValue*  
屬性的值。 *PropertyValue* 是 **nvarchar(max)** 。

## <a name="remarks"></a>備註
有效屬性名稱是 **DisplayName**、**Description**、**Tags**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  

## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格

## <a name="errors-and-warnings"></a>錯誤和警告
  下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限 

-   背景工作代理程式識別碼無效。

-   屬性名稱無效。

-   屬性值無效。  
