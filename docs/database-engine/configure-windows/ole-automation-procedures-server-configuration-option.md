---
title: OLE Automation 程序伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 77e7230fd2b1cbd0513ddec47c8dcb7abc6685ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66775895"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>OLE Automation 程序伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 [OLE Automation 程序]  選項可指定 OLE Automation 物件是否可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次內部啟動。 您也可以使用以原則為基礎的管理或 **sp_configure** 預存程序來設定這個選項。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
 [Ole Automation 程序]  選項可以設定為下列值。  
  
 0  
 停用 OLE Automation Procedures。 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新執行個體的預設值。  
  
 1  
 啟用 OLE Automation Procedures。  
  
 啟用 OLE Automation 程序時，對 **sp_OACreate** 的呼叫會啟動 OLE 共用執行環境。  
  
 您可以使用 **sp_configure** 系統預存程序來檢視和變更 [OLE Automation 程序]  選項目前的值。  
  
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
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
