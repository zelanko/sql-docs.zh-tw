---
title: sp_msx_defect （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5968f8ae8c44f5a20ca93b10c653c950c842cadc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893485"
---
# <a name="sp_msx_defect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從多伺服器作業中移除目前的伺服器。  
  
> [!CAUTION]  
>  **sp_msx_defect**編輯登錄。 您最好不要手動編輯登錄，因為不當或不正確的變更會使系統發生嚴重的組態問題。 因此，只有資深使用者才應該利用登錄編輯器程式來編輯登錄。 如需詳細資訊，請參閱 Microsoft Windows 的文件集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>引數  
`[ @forced_defection = ] forced_defection`指定如果因為將失效損毀的**msdb**資料庫而永久失去主要 SQLServerAgent，或沒有**msdb**資料庫備份，是否要強制脫離。 *forced_defection*是**bit**，預設值是**0**，表示不應執行強制脫離。 值為**1**會強制脫離。  
  
 藉由執行**sp_msx_defect**強制脫離之後，主要 SQLServerAgent 上**系統管理員（sysadmin** ）固定伺服器角色的成員必須執行下列命令來完成脫離：  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 當**sp_msx_defect**正確完成時，就會傳回訊息。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [sp_msx_enlist &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
