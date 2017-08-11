---
title: "指定自訂資料處理延伸模組連接 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fc98f8394e637ea9a627cffd8e40887484462df5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="specify-connections-for-custom-data-processing-extensions"></a>為自訂資料處理延伸模組指定連接
  您可以在報表伺服器中建立或使用協力廠商自訂資料處理延伸模組，以便強化支援之資料來源的資料處理功能，或支援預設 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝未提供的其他資料來源類型。 不同的實作，處理連接的方式也不同。 下列實作適用於資料處理延伸模組：  
  
-   自訂 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者 (若要從 DB2.NET、Oracle、ODP.NET 或 Teradata 資料來源存取資料，您可以使用自訂 .NET 資料提供者)  
  
-   支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>  
  
-   支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>  
  
> [!NOTE]  
>  請洽詢協力廠商提供者，找出自訂資料處理延伸模組的實作方式。  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a>模擬與自訂資料處理延伸模組  
 如果自訂資料處理延伸模組利用模擬連接到資料來源，您必須在 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 或 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 介面使用 Open 方法來提出要求。 此外，您也可以先儲存使用者識別物件 (System.Security.Principal.WindowsIdentity)，然後在其他資料處理延伸模組 API 中重複使用它。  
  
 在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，所有自訂資料處理延伸模組都是在使用者模擬下呼叫。 在此版本中，只有 Open 方法是在模擬使用者時呼叫。 如果您有需要整合式安全性的現有資料處理延伸模組，則必須修改程式碼來使用 Open 方法或儲存使用者識別物件。  
  
## <a name="connections-for-custom-net-framework-data-providers"></a>自訂 .NET Framework 資料提供者的連接  
 設定報表來使用特定資料來源時，您必須設定屬性來判斷資料來源類型、連接字串，以及用於存取資料來源的認證。 下表描述 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者支援的認證類型。 如需設定報表資料來源屬性的詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
|認證|連接|  
|-----------------|-----------------|  
|整合式安全性|如果您的資料提供者支援它，您可以使用 Windows 整合式安全性。 您可以利用目前使用者的認證來傳送要求。<br /><br /> 定義連接字串時，請務必包含指定整合式安全性的引數 (例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 **Integrated Security=SSPI** )。|  
|Windows 驗證|如果您的資料提供者支援它，您可以使用 Windows 網域使用者帳戶。 在呼叫資料處理延伸模組之前，報表伺服器會模擬使用者帳戶。<br /><br /> 定義連接字串時，請務必包含指定整合式安全性的引數 (例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 **Integrated Security=SSPI** )。|  
|資料庫認證|透過自訂 .NET 資料提供者進行的連接不支援資料庫驗證。 在所有情況下，報表伺服器的連接都會失敗。|  
|無認證|您可以搭配自訂 .NET 資料提供者使用 [無認證] 選項。 如果指定自動執行帳戶，連接字串會判斷所使用的認證。 報表伺服器會模擬自動執行帳戶來進行連接。<br /><br /> 如果未定義自動執行帳戶，報表伺服器的連接會失敗。 如需定義帳戶的詳細資訊，請參閱 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。|  
  
## <a name="connections-for-idbconnection"></a>IDbConnection 的連接  
 如果您使用僅支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>的自訂資料處理延伸模組，您必須以下列方式指定連接：  
  
1.  設定自動執行帳戶。 若要利用 **IDbConnection**來進行連接，則必須設定此帳戶。 報表伺服器在進行連接時會模擬該帳戶。  
  
2.  在報表中設定資料來源屬性來使用 **[無認證]**。  
  
3.  將用於連接到資料來源的認證放在連接字串中。  
  
 使用 **IDbConnection**時，不支援下列認證類型：整合式安全性、Windows 使用者帳戶和資料庫認證。 如果資料來源連接使用這些選項，報表伺服器中的連接就會失敗。  
  
## <a name="connections-for-idbconnectionextension"></a>IDbConnectionExtension 的連接  
 如果您使用的是自訂資料處理延伸模組和支援 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>，您必須以下列方式指定連接：  
  
|認證|連接|  
|-----------------|-----------------|  
|整合式安全性|如果您的資料提供者支援它，您可以搭配使用 **IDbConnectionExtension**的自訂資料處理延伸模組來使用 Windows 整合式安全性。<br /><br /> 定義連接字串時，請務必包含指定整合式安全性的引數 (例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 **Integrated Security=SSPI** )。|  
|Windows 驗證|如果您的資料提供者支援它，您可以將 Windows 網域使用者帳戶用於使用 **IDbConnectionExtension**的自訂資料處理延伸模組。<br /><br /> 在呼叫資料處理延伸模組之前，報表伺服器會模擬使用者帳戶。 定義連接字串時，請務必包含指定整合式安全性的引數 (例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的連接可能在連接字串中包含 **Integrated Security=SSPI** )。|  
|資料庫認證|您可以利用資料庫驗證來設定使用 **IDbConnectionExtension**之自訂資料處理延伸模組的連接。|  
|無認證|如果指定自動執行帳戶，連接字串會判斷所使用的認證。<br /><br /> 如果未定義自動執行帳戶，報表伺服器的連接會失敗。|  
  
## <a name="see-also"></a>請參閱＜  
 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [指定認證和報表資料來源的連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [實作資料處理延伸模組](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [報表管理員 &#40;SSRS 原生模式 &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [建立、刪除或修改共用的資料來源 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [設定報表 &#40; 資料來源屬性報表管理員 &#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
