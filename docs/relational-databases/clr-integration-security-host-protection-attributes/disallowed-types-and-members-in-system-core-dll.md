---
title: System.Core.dll 中不允許的類型和成員 |Microsoft Docs
description: SQL Server CLR 程式設計不允許具有 HostProtectionResource 列舉之值的類型或成員。 本文列出 System.Core.dll 不允許的值。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: dcd24cd6-f4ab-42cc-9786-a1604e8a4b4e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b4daca2ced1378057002e40146568a63e3aec39
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727724"
---
# <a name="disallowed-types-and-members-in-systemcoredll"></a>System.Core.dll 中不允許的類型和成員
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通用語言整合（CLR）程式設計不允許使用具有**HostProtectionAttribute**的類型或成員，其指定的**HostProtectionResource**列舉值為**ExternalProcessMgmt**、 **ExternalThreading**、 **MayLeakOnAbort**、 **SecurityInfrastructure**、 **SelfAffectingProcessMgmnt**、 **SelfAffectingThreading**、 **SharedState**、**同步**處理或**UI**。 下表列出 System.Core.dll 組件的成員和類型，這些成員和類型的主機保護屬性 (HPA) 值不被允許。  
  
> [!NOTE]  
>  此清單是根據支援的組件產生的。 如需詳細資訊，請參閱[支援的 .NET Framework 程式庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|類型或成員|HPA 值|  
|--------------------|--------------------|  
|System.Diagnostics.Eventing.EventDescriptor|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProvider|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProviderTraceListener|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEntityAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.WmiConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementMemberAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNewInstanceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementBindAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCreateAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementRemoveAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEnumeratorAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementProbeAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementTaskAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementKeyAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementReferenceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCommitAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNameAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationBaseException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstanceNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventBookmark|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogConfiguration|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogLink|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogStatus|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventProperty|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogPropertySelector|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventKeyword|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLevel|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReader|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogWatcher|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecordWrittenEventArgs|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogSession|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventMetadata|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventOpcode|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventTask|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReadingException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogProviderDisabledException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInvalidDataException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInformation|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.ProviderMetadata|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle|MayLeakOnAbort|  
|System.Security.Cryptography.Aes|MayLeakOnAbort|  
|System.Security.Cryptography.AesCryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.AesManaged|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithm|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithmGroup|MayLeakOnAbort|  
|System.Security.Cryptography.CngKey|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyBlobFormat|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyCreationParameters|MayLeakOnAbort|  
|System.Security.Cryptography.CngProperty|MayLeakOnAbort|  
|System.Security.Cryptography.CngPropertyCollection|MayLeakOnAbort|  
|System.Security.Cryptography.CngProvider|MayLeakOnAbort|  
|System.Security.Cryptography.CngUIPolicy|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellman|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCng|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCngPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsa|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsaCng|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformationCollection|MayLeakOnAbort|  
|System.Security.Cryptography.MD5Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA1Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.StrongNameSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.TimestampInformation|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafePipeHandle|MayLeakOnAbort|  
|System.TimeZoneInfo|MayLeakOnAbort|  
|System.TimeZoneNotFoundException|MayLeakOnAbort|  
|System.InvalidTimeZoneException|MayLeakOnAbort|  
|System.Diagnostics.EventSchemaTraceListener|MayLeakOnAbort|  
|System.Diagnostics.UnescapedXmlDiagnosticData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstanceCounterDataSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstance|MayLeakOnAbort|  
|System.Collections.Generic.HashSet`1|MayLeakOnAbort|  
|System.IO.Pipes.PipeStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.PipeAccessRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeAuditRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeSecurity|MayLeakOnAbort|  
|System.Threading.LockRecursionException|MayLeakOnAbort|  
|System.Threading.ReaderWriterLockSlim|MayLeakOnAbort|  
  
## <a name="see-also"></a>另請參閱  
 [主機保護屬性和 CLR 整合程式設計](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [mscorlib.dll中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.dll中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [在 System.Data.dll 中不允許的類型和成員](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
  
  
