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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a3069bcda85895297626c3f1ec691381e8f071ab
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270959"
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的屬性。

## <a name="syntax"></a>語法

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>引數
[@WorkerAgentId =] *WorkerAgentId*  
Scale Out Worker 的背景工作代理程式識別碼。 *WorkerAgentId* 是 **uniqueidentifier**。

[@PropertyName =] *PropertyName*  
屬性的名稱。 *PropertyName* 是 **nvarchar(256)**。

[@PropertyValue =] *PropertyValue*  
屬性的值。 *PropertyValue* 是 **nvarchar(max)**。

## <a name="remarks"></a>Remarks
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
