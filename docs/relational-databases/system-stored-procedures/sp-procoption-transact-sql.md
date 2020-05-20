---
title: sp_procoption （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 94a5983701bdb7370c389f970d0c75af11a7779c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815222"
---
# <a name="sp_procoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定或清除自動執行預存程序。 每當啟動一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，就會執行一個設為自動執行的預存程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>引數  
`[ @ProcName = ] 'procedure'`這是要設定選項的程式名稱。 程式是**Nvarchar （776）** *，沒有預設*值。  
  
`[ @OptionName = ] 'option'`這是要設定的選項名稱。 [*選項*] 的唯一值是 [**啟動**]。  
  
`[ @OptionValue = ] 'value'`這是指要將選項設定為 on （**true**或**on**）或 off （**false**或**off**）。 *value*是**Varchar （12）**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或錯誤號碼 (失敗)  
  
## <a name="remarks"></a>備註  
 啟動程式必須在**master**資料庫中，而且不能包含輸入或輸出參數。 預存程序會在所有資料庫皆完成復原時執行時，並會在啟動時記錄「已完成復原操作」訊息。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會設定程序自動執行。  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 下列範例會停止程序自動執行。  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
