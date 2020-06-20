---
title: System.Data.dll 中不允許的類型和成員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 6417dfbe000a3c149df8abe80d1fe3b961fc08cf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954252"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>在 System.Data.dll 中不允許的類型和成員
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通用語言整合（CLR）程式設計不允許使用具有之的類型或成員，其 `HostProtectionAttribute` 會指定 `System.Security.Permissions.HostProtectionResource` 具有 `ExternalProcessMgmt` 、 `ExternalThreading` 、、 `MayLeakOnAbort` `SecurityInfrastructure` 、、、 `SelfAffectingProcessMgmnt` `SelfAffectingThreading` **SharedState**、 `Synchronization` 或 `UI` 值的列舉。 下表列出 System.Data.dll 組件的成員和類型，這些成員和類型的主機保護屬性 (HPA) 值不被允許。  
  
> [!NOTE]  
>  此清單是根據支援的組件產生的。 如需詳細資訊，請參閱[支援的 .NET Framework 程式庫](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|類型或成員|HPA 值|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState、Synchronization|  
|System.Xml.XmlDataDocument|同步處理|  
  
## <a name="see-also"></a>另請參閱  
 [主機保護屬性和 CLR 整合程式設計](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll中不允許的類型和成員](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [mscorlib.dll中不允許的類型和成員](disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll中不允許的類型和成員](disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll 中不允許的類型和成員](disallowed-types-and-members-in-system-core-dll.md)  
  
  
