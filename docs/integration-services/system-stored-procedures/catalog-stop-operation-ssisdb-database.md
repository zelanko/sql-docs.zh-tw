---
title: "catalog.stop_operation （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 76a41be8ac6066a4f163b5049a758302d43d5219
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的驗證或執行執行個體。  
  
## <a name="syntax"></a>語法  
  
```sql  
stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>引數  
 [ @operation_id =] *operation_id*  
 驗證或執行執行個體的唯一識別碼。 *Operation_id*是**bigint**。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   驗證或執行執行個體的 READ 和 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   作業識別碼無效  
  
-   作業已停止  
  
## <a name="remarks"></a>備註  
 一次只能有一個使用者停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的作業。 如果多個使用者嘗試停止作業，預存程序將會在第一次嘗試時傳回成功 (值 `0`)，但後續的嘗試將會引發錯誤。  
  
  
