---
title: "Remove-powerpivotserviceapplication 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2742b2a3-927c-4e7c-bd7d-43c072fa01ab
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11219fe0dd15b594d6c59565226e8f25b8259fe8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="remove-powerpivotserviceapplication-cmdlet"></a>Remove-PowerPivotServiceApplication 指令程式

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  刪除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>說明  
 Remove-PowerPivotServiceApplication Cmdlet 會從伺服器陣列中刪除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 使用 DeleteAll 一次刪除所有服務應用程式，或使用 Identity 參數移除單一執行個體。 若要取得執行個體資訊，請執行 Get-PowerPivotServiceApplication 以傳回伺服器陣列中的所有執行個體。  
  
 使用 RemoveData 參數可以選擇性地移除服務應用程式資料庫和快取檔案。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 一旦移除服務應用程式之後，活頁簿會保留在內容庫中，但不再運作。  
  
## <a name="parameters"></a>參數  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>識別\<SPGeminiServiceApplicationPipeBind >  
 指定伺服器陣列中單一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式的 GUID。 如果您只要移除一個應用程式，讓其他服務應用程式保持不變，則必須指定 GUID。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
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
  
### <a name="-deleteall-switch"></a>-Deleteall 一樣\<切換 >  
 刪除所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，但不刪除服務應用程式資料庫，也不刪除伺服器陣列中的服務執行個體物件。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 在移除服務應用程式之後，系統服務和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 引擎服務物件會保持具現化，但無法使用。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-removedata-switch"></a>-RemoveData\<切換 >  
 移除包含下列項目的服務應用程式資料庫：資料重新整理排程、活頁簿使用量資料、用於追蹤哪些資料庫已載入的執行個體對應，以及其他內部資料。  
  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 此範例會刪除單一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式，但不會移除其資料庫或快取。 如果未指定識別，系統會提示您提供識別。  
  
## <a name="example-2"></a>範例 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 此範例會刪除伺服器陣列中的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。 資料庫和快取不會被刪除。  
  
## <a name="example-3"></a>範例 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 此範例會刪除單一 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式以及其資料庫與快取檔案。  
  
  
