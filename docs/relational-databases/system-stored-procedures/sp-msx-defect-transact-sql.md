---
description: sp_msx_defect (Transact-SQL)
title: sp_msx_defect (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1b5ea1139e0cfc1b27d7b79df29e6c1b1381b4d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541535"
---
# <a name="sp_msx_defect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從多伺服器作業中移除目前的伺服器。  
  
> [!CAUTION]  
>  **sp_msx_defect** 編輯登錄。 您最好不要手動編輯登錄，因為不當或不正確的變更會使系統發生嚴重的組態問題。 因此，只有資深使用者才應該利用登錄編輯器程式來編輯登錄。 如需詳細資訊，請參閱 Microsoft Windows 的文件集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>引數  
`[ @forced_defection = ] forced_defection` 指定當主要 SQLServerAgent 因為將失效損毀的 **msdb** 資料庫或沒有 **msdb** 資料庫備份而永久遺失時，是否要強制脫離。 *forced_defection*是 **bit**，預設值是 **0**，表示不應該進行強制脫離。 **1**值強制脫離。  
  
 執行 **sp_msx_defect**強制執行脫離之後，主要 SQLServerAgent 的 **系統管理員（sysadmin** ）固定伺服器角色的成員必須執行下列命令來完成脫離：  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 當 **sp_msx_defect** 正確完成時，會傳回訊息。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [sp_msx_enlist &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
