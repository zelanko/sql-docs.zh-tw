---
title: OLE Automation 程序伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d8a01c5bf886006e2f4eb6a352ea7f2a7b43ac29
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055998"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>OLE Automation 程序伺服器組態選項
  使用 `Ole Automation Procedures` 選項可指定 OLE Automation 物件是否可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次內部啟動。 您也可以使用以原則為基礎的管理或 **sp_configure** 預存程序來設定這個選項。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
 `Ole Automation Procedures`選項可以設定為下列值。  
  
 0  
 停用 OLE Automation Procedures。 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新執行個體的預設值。  
  
 1  
 啟用 OLE Automation Procedures。  
  
 啟用 OLE Automation 程序時，對 **sp_OACreate** 的呼叫會啟動 OLE 共用執行環境。  
  
 目前的值`Ole Automation Procedures`選項可以檢視和使用變更**sp_configure**系統預存程序。  
  
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
  
  
