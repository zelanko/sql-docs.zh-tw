---
title: "Remove-powerpivotsystemserviceinstance 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e44d28106db0c14c293c463d91125b262190350d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Remove-PowerPivotSystemServiceInstance 指令程式

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  從伺服器陣列中移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>說明  
 Remove-PowerPivotSystemServiceInstance Cmdlet 會從伺服器陣列中移除有關 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務的執行個體資訊。 它不會移除程式檔案。 若要永久移除程式檔案，您必須先將這些檔案解除安裝。  
  
 如果您移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務，請務必也執行 Remove-PowerPivotEngineServiceInstance，以移除相關聯的 Analysis Services 執行個體，接著執行 Remove-PowerPivotServiceApplication 以刪除任何 PowerPivot 服務應用程式。 一旦移除服務之後，服務應用程式將不再執行。  
  
 若要還原此變更，您可以執行 New-PowerPivotSystemServiceInstance -Provision:$true 以重新啟用執行個體資訊。  
  
## <a name="parameters"></a>參數  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>識別\<PowerPivotMidTierServiceInstancePipeBind >  
 指定要移除之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體的 GUID。 安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的每部應用程式伺服器上都有一個服務執行個體。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal\<切換 >  
 刪除本機電腦上安裝的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體，讓您不需要指定物件識別即可移除執行個體。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
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
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 這個範例示範如何移除本機應用程式伺服器上執行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體。  
  
## <a name="example-2"></a>範例 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 這個範例示範如何根據識別刪除特定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務。  
  
  

