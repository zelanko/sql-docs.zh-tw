---
title: "Set-powerpivotsystemservice 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: f6ef197b-3d74-4339-ae73-8a7c1eaf0e91
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a3d63834fe9322f45d0524de5434154f1257056
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="set-powerpivotsystemservice-cmdlet"></a>Set-PowerPivotSystemService 指令程式
  
  [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]
  
  在伺服器陣列層級設定 PowerPivotSystemService 物件的全域屬性。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
Set-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [-UpdateAssemblyInformation <switch>] [-WorkbookUpgradeOnDataRefresh <boolean>] [-DirectTCPConnections <boolean>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>說明  
 Set-PowerPivotSystemService 指令程式會更新伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務父物件的屬性。  
  
## <a name="parameters"></a>參數  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>識別\<PowerPivotMidTierServicePipeBind >  
 指定要更新屬性的父物件。 此值必須是可在伺服器陣列中唯一識別物件的有效 GUID。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="-updateassemblyinformation-switch"></a>-UpdateAssemblyInformation\<切換 >  
 僅用於升級。 如果伺服器陣列中部署的組件版本不同於 SharePoint 組態資料庫中儲存的版本，您可以執行此指令程式以更新組態資料庫中的組件資訊。 可在全域組件中儲存之 Microsoft.AnalysisServices.SharePoint.Integration.dll 檔案的檔案屬性中找到組件版本資訊。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-workbookupgradeondatarefresh-boolean"></a>-WorkbookUpgradeOnDataRefresh\<布林值 >  
 可在開始進行伺服器上排定之資料重新整理時，用來自動升級 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 活頁簿。 只有符合伺服器目前版本的活頁簿才支援資料重新整理。 如果啟用此屬性，活頁簿將自動升級，以便繼續該資料重新整理。 此屬性是在伺服器執行個體層級上設定。 您不能為特定活頁簿、文件庫、網站或使用者變更它。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|2|  
|預設值|false|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-directtcpconnections-boolean"></a>-DirectTCPConnections\<布林值 >  
 指定 Excel Services 將所有查詢直接傳送至載入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫的 SQL Server Analysis Services (POWERPIVOT) 執行個體，略過通常在每個查詢要求傳送至 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫時都會使用的 MSOLAP 資料提供者和通道傳輸。  
  
 設定此參數，可更有效率地連接到載入的資料庫，改進 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查詢的效能和延展性。 請注意，此參數不會變更初始載入要求如何配置的行為。 其他參數如 -RoundRobinAllocation 和 -HealthBasedAllocation 等不受影響 (其用於在伺服器陣列中多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 執行個體之間配置資料庫載入要求)，因為 -DirectTCPConnections 只套用至載入資料庫之後發出的查詢。  
  
 伺服器陣列拓撲若包含在不同應用程式伺服器上執行的 Excel Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，您必須在防火牆開啟通訊埠，以確保要求會到達 SQL Server Analysis Services (POWERPIVOT) 執行個體。 如需如何為 Analysis Services 具名執行個體啟用傳入連接的指示，請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|3|  
|預設值|false|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-confirm-switch"></a>確認\<切換 >  
 在執行命令之前提示您確認。 此值預設是啟用的。 若要在命令中略過確認回應，請在命令上指定 Confirm:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
C:\PS>Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true  
```  
  
 啟用舊版活頁簿的自動升級，以便繼續執行排定的資料重新整理。  
  
  
