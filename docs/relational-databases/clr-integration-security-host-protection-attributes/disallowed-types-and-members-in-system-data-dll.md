---
title: 型別和成員在 System.Data.dll 中不允許 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 50f7f8aacfc61b55e969ea0d57f82d58e50e093b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028125"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>在 System.Data.dll 中不允許的類型和成員
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] common language integration (CLR) 程式設計不允許使用型別或成員具有**HostProtectionAttribute** ，指定**System.Security.Permissions.HostProtectionResource**列舉值是**ExternalProcessMgmt**， **ExternalThreading**， **MayLeakOnAbort**， **SecurityInfrastructure**， **SelfAffectingProcessMgmnt**， **SelfAffectingThreading**， **SharedState**，**同步處理**，或**UI**。 下表列出 System.Data.dll 組件的成員和類型，這些成員和類型的主機保護屬性 (HPA) 值不被允許。  
  
> [!NOTE]  
>  此清單是根據支援的組件產生的。 如需詳細資訊，請參閱 <<c0> [ 支援的.NET Framework 程式庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|類型或成員|HPA 值|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState、Synchronization|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>另請參閱  
 [主機保護屬性和 CLR 整合程式設計](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Mscorlib.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
