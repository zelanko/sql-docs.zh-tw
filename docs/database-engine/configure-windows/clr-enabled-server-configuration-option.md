---
title: "CLR 已啟用伺服器組態選項 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1a07df55338a75d43937f4571c6c899d9bb6add2
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="clr-enabled-server-configuration-option"></a>CLR 已啟用伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 clr enabled 選項來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否能執行使用者組件。 [CLR 已啟用] 選項提供下列值： 
  
|值|描述|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上不允許組件執行。|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上允許組件執行。|  
  
僅限 WOW64。 請重新啟動 WOW64 伺服器使設定變更生效。 對於其他伺服器類型，則不需要重新啟動。  

當您執行 RECONFIGURE 且 [CLR 已啟用] 選項的執行值從 1 變更為 0 時，會立即卸載包含使用者組件的所有應用程式定義域。  
  
>  **在輕量型共用下，不支援 Common Language Runtime (CLR) 執行：** 請停用下列兩個選項的其中之一：[CLR 已啟用] 或 [輕量型共用]。 依賴 CLR 而且在 Fiber 模式下無法正常運作的功能包括了 **階層** 資料類型、複寫和原則式管理。  

>  [!WARNING]
>  CLR 使用 .NET Framework 中的程式碼存取安全性 (CAS)，而這不再支援為安全性界限。 使用 `PERMISSION_SET = SAFE` 所建立的 CLR 組件可能可以存取外部系統資源、呼叫 Unmanaged 程式碼，以及需要 sysadmin 權限。 從 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 開始，引進稱為 `clr strict security` 的 `sp_configure` 選項，來增強 CLR 組件的安全性。 `clr strict security` 預設會予以啟用，並將 `SAFE` 和 `EXTERNAL_ACCESS` 組件視為就像標示上 `UNSAFE` 一樣。 可以基於回溯相容性停用 `clr strict security` 選項，但不建議這麼做。 Microsoft 建議透過具有已獲授與 master 資料庫中 `UNSAFE ASSEMBLY` 權限之對應登入的憑證或非對稱金鑰簽署所有組件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員也可以將組件新增至資料庫引擎應該信任的組件清單。 如需詳細資訊，請參閱 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)。
  
## <a name="example"></a>範例  
 以下範例會先顯示使用 clr 已啟用選項的目前設定，然後將選項值設定為 1 來啟用選項。 若要停用此選項，請將值設定為 0。  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## <a name="see-also"></a>另請參閱  
 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  

