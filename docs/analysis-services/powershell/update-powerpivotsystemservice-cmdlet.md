---
title: "Update-PowerPivotSystemService 指令程式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: a90f1158-68d3-4330-98c1-fb0f81e13328
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Update-PowerPivotSystemService 指令程式
  升級伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務父物件。  
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## 語法  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## 說明  
 **Update-PowerPivotSystemService** Cmdlet 會在伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務父物件、執行個體和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式上執行一系列升級動作。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署中所有的中間層服務和應用程式都必須在相同的功能等級執行。 這個指令程式會在所有這些物件上執行升級動作。  
  
 在執行 SQL Server 安裝程式以安裝新版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 之後，或在伺服器上套用累積更新之後，就可以執行這個 Cmdlet 。 若要檢查是否需要進行升級，請執行 `Get-PowerPivotSystemService` 檢閱 **NeedsUpgrade** 屬性。 如果 **NeedsUpgrade** 為 true，則應該執行此 Cmdlet，以升級伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中間層物件。  
  
 因為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署包含中間層和後端資料服務，所以在執行 **Update-PowerPivotSystemService** 時必須執行 **Update-PowerPivotEngineService**，以確保伺服器陣列中的這兩層都是相同版本。  
  
 升級無法回復到舊版。 如果您必須還原為舊版，請從 SharePoint 伺服器陣列中移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]，然後重新安裝軟體。 若要確認升級作業是否成功，請執行 `Get-PowerPivotSystemService` 檢閱全域屬性中的版本資訊，並確認 **NeedsUpgrade** 已不再設為 true。  
  
## 參數  
  
### -Confirm \<switch>  
 在執行命令之前提示您確認。 此值預設是啟用的。 若要在命令中略過確認回應，請在命令上指定 Confirm:$false。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### \<CommonParameters>  
 這個指令程式支援下列參數：  
  
-   [詳細資訊]  
  
-   偵錯  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無。|  
  
  