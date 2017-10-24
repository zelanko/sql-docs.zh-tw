---
title: "catalog.set_worker_agent_property （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: c1caf4a71e5802968d9471711b8206a26f9c28d5
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

設定的屬性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]標尺出背景工作。

## <a name="syntax"></a>語法

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>引數
[@WorkerAgentId =] *WorkerAgentId*  
背景工作代理程式識別碼的標尺出背景工作。 *WorkerAgentId*是**uniqueidentifier**。

[@PropertyName =] *PropertyName*  
屬性的名稱。 *PropertyName*是**nvarchar （256)**。

[@PropertyValue =] *PropertyValue*  
屬性的值。 *PropertyValue*是**nvarchar （max)**。

## <a name="remarks"></a>備註
有效的屬性名稱都是**DisplayName**，**描述**，**標記**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色

## <a name="errors-and-warnings"></a>錯誤和警告
  下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限 

-   背景工作代理程式識別碼無效。

-   屬性名稱無效。

-   屬性值無效。  
