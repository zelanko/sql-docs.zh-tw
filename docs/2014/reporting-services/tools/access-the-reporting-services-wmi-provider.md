---
title: 存取 Reporting Services WMI 提供者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- Reporting Services WMI Provider
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
caps.latest.revision: 55
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 6c3c4bb9cc188e08ad38de73c2be4949e4c6afab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022807"
---
# <a name="access-the-reporting-services-wmi-provider"></a>存取 Reporting Services WMI 提供者
  Reporting Services WMI 提供者會公開兩個 WMI 類別，可透過指令碼管理原生模式報表伺服器執行個體：  
  
> [!IMPORTANT]  
>  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版開始，只有原生模式報表伺服器才支援 WMI 提供者。 SharePoint 模式報表伺服器可以透過 SharePoint 管理中心頁面和 PowerShell 指令碼管理。  
  
|類別|命名空間|描述|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName >* \v11|提供用戶端連接至已安裝之報表伺服器所需的基本資訊。|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName >* \v11\Admin|代表報表伺服器執行個體的安裝與執行階段參數。 這些參數是儲存在報表伺服器的組態檔中。<br /><br /> **\*\* 重要事項 \*\*** 這個類別只能透過管理權限存取。|  
  
 針對每一個報表伺服器執行個體會建立上述每一個類別的執行個體。 您可以使用任何 Microsoft 或協力廠商工具來存取報表伺服器公開的 WMI 物件，包括 .NET Framework 本身公開的 WMI 程式開發介面。 本主題描述如何存取及使用 WMI 類別執行個體搭配 PowerShell 命令 [Get-WmiObject](http://technet.microsoft.com/library/dd315295.aspx)。  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>判斷命名空間字串中的執行個體名稱  
 命名空間路徑中 Reporting Services WMI 類別的執行個體名稱，是您安裝具名 Reporting Services 執行個體時指定的執行個體名稱編碼。 也就是說，執行個體名稱中的特殊字元會經過編碼。 例如，底線 (_) 會編碼為 "_5f"，因此 "My_Instance" 這個執行個體名稱在 WMI 命名空間路徑中就會編碼為 "My_5fInstance"。  
  
 若要列出 WMI 命名空間路徑中報表伺服器執行個體的編碼執行個體名稱，請使用下列 PowerShell 命令：  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace root\Microsoft\SqlServer\ReportServer  –class __Namespace –ComputerName hostname | select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>使用 PowerShell 存取 WMI 類別  
 若要存取 WMI 類別，請執行下列命令：  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace <namespacename> –class <classname> –ComputerName <hostname>  
```  
  
 例如，若要存取主機 myrshost 的預設報表伺服器執行個體上的 MSReportServer_ConfigurationSetting 類別，請執行下列命令。 預設報表伺服器執行個體必須安裝在 myrshost 上，這個命令才會成功。  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 這個命令語法會輸出所有類別屬性名稱和值。 請注意，即使您是存取預設報表伺服器執行個體 (RS_MSSQLSERVER) 的命名空間中的類別，仍會傳回 MSReportServer_ConfigurationSetting 類別的所有執行個體。 例如，如果 myrshost 上安裝了預設報表伺服器執行個體和名為 SHAREPOINT 的具名報表伺服器執行個體，則這個命令將傳回兩個 WMI 物件，並輸出這兩個報表伺服器執行個體的屬性名稱和值。  
  
 若要在傳回多個執行個體時傳回特定類別的執行個體，請使用 –Filter 參數，依據擁有唯一值的屬性 (例如 InstanceName) 篩選結果。 例如，若只要傳回預設報表伺服器執行個體的 WMI 物件，請使用下列命令：  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>查詢可用的方法和屬性  
 若要查看其中一個 Reporting Services WMI 類別中可用的方法和屬性，請將結果從 Get-WmiObject 管道傳送到 Get-Member 命令。 例如：  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
 如需 Reporting Services WMI 類別之屬性和方法的文件，請參閱 ...。  
  
## <a name="use-a-wmi-method-or-property"></a>使用 WMI 方法或屬性  
 您具有 Reporting Services 類別的 WMI 物件並且知道可用的方法和屬性之後，就可以使用這些方法和屬性。 例如，如果您擁有名為 SHAREPOINT 的 SharePoint 整合模式具名報表伺服器執行個體，請使用下列命令序列擷取 SharePoint 管理中心網站的 URL：  
  
```  
PS C:\windows\system32> $rsconfig = Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='SHAREPOINT'"  
PS C:\windows\system32> $rsconfig.GetAdminSiteUrl()  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services WMI 提供者程式庫參考&#40;SSRS&#41;](../wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [RSReportServer 組態檔](../report-server/rsreportserver-config-configuration-file.md)  
  
  