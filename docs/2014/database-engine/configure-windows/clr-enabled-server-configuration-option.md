---
title: CLR 已啟用伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45c72bc5b811fec8e5532d5d03d4552cc2e0d319
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786677"
---
# <a name="clr-enabled-server-configuration-option"></a>CLR 已啟用伺服器組態選項
  使用 clr enabled 選項來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是否能執行使用者組件。 clr enabled 選項提供下列值。  
  
|值|描述|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上不允許組件執行。|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上允許組件執行。|  
  
 WOW64 伺服器必須重新啟動之後，對此設定的變更才能生效。 對於其他伺服器類型，則不需要重新啟動。  
  
> [!NOTE]  
>  執行 RECONFIGURE 且 clr enabled 選項的執行值從 1 變更為 0 時，會立即卸載包含使用者組件的所有應用程式網域。  
  
> [!NOTE]  
>  輕量型共用不支援 Common Language Runtime (CLR) 的執行。 停用下列一或兩個選項："clr enabled" 或 "lightweight pooling"。 依賴 CLR 而且在 Fiber 模式下無法正常運作的功能包括 `hierarchy` 資料類型、複寫和以原則為基礎的管理。  
  
## <a name="example"></a>範例  
 以下範例會先顯示使用 clr 已啟用選項的目前設定，然後將選項值設定為 1 來啟用選項。 若要停用此選項，請將值設定為 0。  
  
```  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [輕量型共用伺服器組態選項](lightweight-pooling-server-configuration-option.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [輕量型共用伺服器組態選項](lightweight-pooling-server-configuration-option.md)  
  
  
