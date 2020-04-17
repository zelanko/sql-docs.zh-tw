---
title: 管理 CLR 整合程式集 |微軟文件
description: 您可以在 SQL Server 中託管託管 DLL 程式集。  您可以註冊、更改和刪除程式集,還可以管理關聯的文件和許可權。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: 19b90d7994aa4b75a294f24345d43333d13a22df
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484727"
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 整合組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Managed 程式碼會經過編譯，然後以稱為組件的單位進行部署。 組件會封裝為 DLL 或可執行檔 (.exe)。 可執行檔可以自行執行，而 DLL 則必須裝載在現有的應用程式中。 託管 DLL 程式集可以載入到[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中 並由 承載。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會先要求您使用 CREATE ASSEMBLY 陳述式，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，然後才可以載入到處理序中使用。 這些組件也可以使用 ALTER ASSEMBLY 陳述式，從比較新的版本升級，或者使用 DROP ASSEMBLY 陳述式，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 移除。  
  
 程式集資訊存儲在已安裝程式集的資料庫中的**sys.assembly_files**表中。 **sys.assembly_files**表包含以下列。  
  
|資料行|描述|  
|------------|-----------------|  
|assembly_id|為組件定義的識別項。 此號碼會指派給與同一組件相關的所有物件。|  
|NAME|物件的名稱。|  
|file_id|標識每個物件的數位,第一個與給定**assembly_id**關聯的物件被給定值為 1。 如果多個物件與同一**個assembly_id**相關聯,則每個後續**file_id**值將遞增 1。|  
|content|組件或檔案的十六進位表示法。|  
  
## <a name="in-this-section"></a>本節內容  
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 討論如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立 SAFE、EXTERNAL_ACCESS 與 UNSAFE CLR 組件。  
  
 [變更組件](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 組件。  
  
 [卸除組件](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 討論如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 卸除 CLR 組件。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
