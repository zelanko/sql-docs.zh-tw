---
title: "管理 CLR 整合組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0e533e43c49bcd7bc32264cf1e59216ee0bc03a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 整合組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Managed 程式碼編譯並再稱為組件的單元中進行部署。 組件會封裝為 DLL 或可執行檔 (.exe)。 可執行檔可以自行執行，而 DLL 則必須裝載在現有的應用程式中。 Managed 的 DLL 組件可以載入並由[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會先要求您使用 CREATE ASSEMBLY 陳述式，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，然後才可以載入到處理序中使用。 這些組件也可以使用 ALTER ASSEMBLY 陳述式，從比較新的版本升級，或者使用 DROP ASSEMBLY 陳述式，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 移除。  
  
 組件資訊會儲存在**sys.assembly_files**資料庫已安裝的組件中的資料表。 **Sys.assembly_files**資料表包含下列資料行。  
  
|「資料行」|描述|  
|------------|-----------------|  
|assembly_id|為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。|  
|NAME|物件的名稱。|  
|file_id|數字，識別每個物件，與相關聯的第一個物件指定**assembly_id**給定值為 1。 如果多個物件具有相同相關**assembly_id**，則每個後續**file_id**值都會遞增 1。|  
|content|組件或檔案的十六進位表示法。|  
  
## <a name="in-this-section"></a>本節內容  
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 討論如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立 SAFE、EXTERNAL_ACCESS 與 UNSAFE CLR 組件。  
  
 [變更組件](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 組件。  
  
 [卸除組件](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 討論如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 卸除 CLR 組件。  
  
## <a name="see-also"></a>請參閱  
 [CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
