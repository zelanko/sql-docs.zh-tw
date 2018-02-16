---
title: New-PowerPivotSystemServiceInstance cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2e412047e4d859de637da933d2335232961ee13
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>New-PowerPivotSystemServiceInstance 指令程式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務的新執行個體加入至應用程式伺服器中。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 在本機應用程式伺服器上使用 SQL Server 安裝程式安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 之後，使用 New-PowerPivotSystemServiceInstance Cmdlet 在伺服器陣列層級佈建新的 PowerPivotSystemService 物件。 每個應用程式伺服器上只能佈建一個服務執行個體。  如果已佈建此服務，則無法執行這個指令程式。  
  
## <a name="parameters"></a>參數  
  
### <a name="-parentservice-powerpivotmidtierservicepipebind"></a>-ParentService \<PowerPivotMidTierServicePipeBind>  
 指定伺服器陣列中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務父物件的 GUID。 在此版本中，只允許一個父物件。 您可以使用 Get-PowerPivotSystemService 傳回服務物件或其 GUID。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="-systemserviceinstancename-string"></a>-SystemServiceInstanceName \<string>  
 指定識別此物件的名稱。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="provision-switchparameter"></a>佈建 [\<SwitchParameter >]  
 讓 SharePoint 可使用服務。 有效值為 $true 或 $false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 這個指令程式支援一般參數：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 這個範例示範此指令程式最常見的形式。 它會向伺服器陣列註冊本機應用程式伺服器上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務。  
  
## <a name="example-2"></a>範例 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 這個範例會為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體命名，但不會佈建它。 如果未提供名稱，則會改用預設名稱「SQL Server Analysis Services 系統服務執行個體」。 建立自訂服務名稱是選擇性的。 若要支援測試案例，或者如果有自訂工具或指令碼可在稍後步驟中佈建執行個體，您可以為服務命名。  
  
  
