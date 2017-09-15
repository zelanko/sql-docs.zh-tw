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
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d0476bbb67cff44a05aed1441a31d679882b4cb3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

設定的屬性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]標尺出背景工作。

## <a name="syntax"></a>語法

```tsql
set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId, [ @PropertyName = ] PropertyName, [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>引數
[ @WorkerAgentId =] *WorkerAgentId*  
標尺出背景工作的背景工作代理程式識別碼。 *WorkerAgentId*是**uniqueidentifier**。

[ @PropertyName =] *PropertyName*  
屬性的名稱。 *PropertyName*是**nvarchar （256)**。

[ @PropertyValue =] *PropertyValue*  
屬性值。 *PropertyValue*是**nvarchar （max)**。

## <a name="remarks"></a>備註
有效的屬性名稱是**DisplayName**，**描述**，**標記**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色

## <a name="erros-and-warnings"></a>錯誤和警告
  下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限 

-   背景工作代理程式識別碼無效。

-   屬性名稱無效。

-   屬性值不是 vilid。  
