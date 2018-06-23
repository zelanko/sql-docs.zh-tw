---
title: 管理 CLR 整合組件 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3cc471d26701fb71cac53645ee16d4f5bff41c44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133522"
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 整合組件
  Managed 程式碼會經過編譯，然後以稱為組件的單位進行部署。 組件會封裝為 DLL 或可執行檔 (.exe)。 可執行檔可以自行執行，而 DLL 則必須裝載在現有的應用程式中。 Managed 的 DLL 組件可以載入並由[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 CREATE ASSEMBLY 陳述式之前將它載入到處理序，並使用資料庫。 這些組件也可以使用 ALTER ASSEMBLY 陳述式，從比較新的版本升級，或者使用 DROP ASSEMBLY 陳述式，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 移除。  
  
 組件資訊會儲存在安裝該組件所在資料庫的 `sys.assembly_files` 資料表中。 `sys.assembly_files` 資料表包含下列資料行。  
  
|「資料行」|描述|  
|------------|-----------------|  
|assembly_id|為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。|  
|NAME|物件的名稱。|  
|file_id|識別每個物件的數字，其中會將 1 的值指派給與給定 `assembly_id` 相關聯的第一個物件。 如果有多個物件與相同的 `assembly_id` 相關聯，則每個後續的 `file_id` 值都會以 1 遞增。|  
|content|組件或檔案的十六進位表示法。|  
  
## <a name="in-this-section"></a>本節內容  
 [建立組件](creating-an-assembly.md)  
 討論如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立 SAFE、EXTERNAL_ACCESS 與 UNSAFE CLR 組件。  
  
 [變更組件](altering-an-assembly.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 組件。  
  
 [卸除組件](dropping-an-assembly.md)  
 討論如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 卸除 CLR 組件。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../security/clr-integration-security.md)   
 [CLR 整合程式碼存取安全性](../security/clr-integration-code-access-security.md)  
  
  