---
title: sp_enumdsn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30aa77cb33e5d55bef6b110e020116467536eaff
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031070"
---
# <a name="spenumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對特定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶所執行的伺服器，傳回所有已定義之 ODBC 和 OLE DB 資料來源名稱的清單。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資料來源名稱**|**sysname**|資料來源的名稱。|  
|**說明**|**varchar(255)**|資料來源的描述。|  
|**型別**|**int**|資料來源的類型：<br /><br /> **1** = ODBC 資料來源名稱<br /><br /> **3** = OLE DB 資料來源|  
|**提供者名稱**|**varchar(255)**|OLE DB 提供者的名稱。 ODBC DSN 的這個值是 NULL。|  
  
## <a name="remarks"></a>備註  
 每隔[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務有一個使用者內容。 使用者內容是一組登錄項目，其中包括使用者 ODBC 資料來源的定義。 使用者內容由執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者名稱提供。  
  
 例如，如果伺服器是利用系統帳戶使用者內容來執行的，傳回的資料來源名稱 (DSN) 便全為系統帳戶所關聯的系統 DSN。 如果是以私用使用者帳戶來執行伺服器，則只會傳回這位使用者的私用帳戶所定義之 DSN。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_enumdsn**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dsninfo &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
