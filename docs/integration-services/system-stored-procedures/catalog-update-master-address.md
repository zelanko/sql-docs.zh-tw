---
title: "catalog.update_master_address （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e5e560d6011370b3d56ba13c86608d2be3d0dc6e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address （SSISDB 資料庫）
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

更新[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]標尺出主要端點。

## <a name="syntax"></a>語法

```sql
update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>引數
[ @MasterAddress =] *masterAddress*  
標尺出主要端點。 *MasterAddress*是**nvarchar**。  

 ## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  

## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
   
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
 
