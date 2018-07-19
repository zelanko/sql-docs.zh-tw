---
title: catalog.update_master_address (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 50953f913101cf4ec08bf492034abb1d5e43da40
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406920"
---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 主端點。

## <a name="syntax"></a>語法

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>引數
[ @MasterAddress = ] *masterAddress*  
Scale Out 主端點。 *masterAddress* 是 **nvarchar**。  

 ## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
   
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
 
