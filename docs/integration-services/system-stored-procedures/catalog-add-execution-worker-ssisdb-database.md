---
title: catalog.add_execution_worker (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: chugugrace
ms.author: chugu
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d68d8675f6ddc703af982102a0017e7920790b72
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749746"
---
# <a name="catalogadd_execution_worker-ssisdb-database"></a>catalog.add_execution_worker (SSISDB 資料庫)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/applies-to-version/sqlserver2017.md)]

將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 新增 Scale Out 中的執行個體。

## <a name="syntax"></a>語法

```sql
catalog.add_execution_worker [ @execution_id = ] execution_id, [ @workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>引數
[ @execution_id = ] *execution_id*  
 執行之執行個體的唯一識別碼。 *execution_id* 是 **bigint**。  
 
[@workeragent_id = ] *workeragent_id*  
Scale Out Worker 的背景工作代理程式識別碼。 *workeragent_id* 是 **uniqueidentifier**。

## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  

## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
 
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
 
- 使用者未具備適當的權限。

- 執行識別碼無效。

- 背景工作代理程式識別碼無效。

- 執行不是在 Scale Out 中。

## <a name="see-also"></a>另請參閱
[在 Scale Out 中執行套件](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)。

