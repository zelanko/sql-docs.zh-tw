---
description: xp_logevent (Transact-SQL)
title: xp_logevent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7001b9d29a96dd192e044ddfe779b8f39a581a94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419272"
---
# <a name="xp_logevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔和 Windows 事件檢視器中記錄使用者定義的訊息。 xp_logevent 可以用來傳送警示，而不需要傳送訊息給用戶端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>引數  
 *error_number*  
 這是使用者自訂的錯誤號碼 (大於 50,000)。 最大值是 2147483647 (2^31 - 1)。  
  
 **'** *message* **'**  
 這是字元字串，最多 2048 個字元。  
  
 **'** *嚴重性* **'**  
 這是三個字元字串的其中一個：INFORMATIONAL、WARNING 或 ERROR。 *嚴重性* 是選擇性的，預設值是 [資訊]。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 xp_logevent 會針對所包含的程式碼範例，傳回下列錯誤訊息：  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>備註  
 當您從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式、觸發程式、批次等傳送訊息時，請使用 RAISERROR 語句，而不是 xp_logevent。 xp_logevent 不會呼叫用戶端的訊息處理常式或設定 @ @ERROR 。 若要將訊息寫入 Windows 事件檢視器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中，請執行 RAISERROR 陳述式。  
  
## <a name="permissions"></a>權限  
 需要 master 資料庫中 db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將訊息連同傳遞到訊息的變數記錄到 Windows 事件檢視器中。  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>另請參閱  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的一般擴充預存程式 ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
