---
description: sp_enumdsn (Transact-SQL)
title: sp_enumdsn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: afc6b97a969aa833e96bd4d8c2ad1a35ae35d14b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469480"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對特定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶所執行的伺服器，傳回所有已定義之 ODBC 和 OLE DB 資料來源名稱的清單。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資料來源名稱**|**sysname**|資料來源的名稱。|  
|**說明**|**varchar(255)**|資料來源的描述。|  
|**型別**|**int**|資料來源的類型：<br /><br /> **1** = ODBC DSN<br /><br /> **3** = OLE DB 資料來源|  
|**提供者名稱**|**varchar(255)**|OLE DB 提供者的名稱。 ODBC DSN 的這個值是 NULL。|  
  
## <a name="remarks"></a>備註  
 每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務都有一個使用者內容。 使用者內容是一組登錄項目，其中包括使用者 ODBC 資料來源的定義。 使用者內容由執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者名稱提供。  
  
 例如，如果伺服器是利用系統帳戶使用者內容來執行的，傳回的資料來源名稱 (DSN) 便全為系統帳戶所關聯的系統 DSN。 如果是以私用使用者帳戶來執行伺服器，則只會傳回這位使用者的私用帳戶所定義之 DSN。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_enumdsn**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dsninfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
