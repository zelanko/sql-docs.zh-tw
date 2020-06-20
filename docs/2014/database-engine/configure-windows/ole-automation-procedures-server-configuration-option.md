---
title: OLE Automation 程序伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d34615ce1f808c1015c9c3d312a38a67dba291b4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935189"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>OLE Automation 程序伺服器組態選項
  使用 `Ole Automation Procedures` 選項可指定 OLE Automation 物件是否可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次內部啟動。 您也可以使用以原則為基礎的管理或 **sp_configure** 預存程序來設定這個選項。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
 `Ole Automation Procedures` 選項可設定為下列值：  
  
 0  
 停用 OLE Automation Procedures。 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新執行個體的預設值。  
  
 1  
 啟用 OLE Automation Procedures。  
  
 啟用 OLE Automation 程序時，對 **sp_OACreate** 的呼叫會啟動 OLE 共用執行環境。  
  
 您 `Ole Automation Procedures` 可以使用**sp_configure**系統預存程式，來查看和變更選項的目前值。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何檢視 OLE Automation Procedures 的目前設定。  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 下列範例顯示如何啟用 OLE Automation Procedures。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [介面區組態](../../relational-databases/security/surface-area-configuration.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
