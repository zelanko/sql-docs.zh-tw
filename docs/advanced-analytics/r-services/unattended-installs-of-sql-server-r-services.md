---
title: "SQL Server R Services 的自動安裝 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server R Services 的自動安裝
    
開始之前的安裝程序，請注意下列需求︰

+ 您必須在安裝資料庫引擎，您將在其中使用 R 服務 （資料庫） 的每個執行個體 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
+ 如果您正在執行離線安裝，您必須事先下載必要的 R 元件，並將它們複製到本機資料夾。 如需下載位置，請參閱 [安裝 R 元件無法存取網際網路](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。   
+ 沒有新的參數， */IACCEPTROPENLICENSETERMS*, ，表示您接受授權合約的使用開放原始碼 R 元件。 如果您未在命令列中包含此參數，安裝程式將會失敗。  
  
## 執行 R Services 的自動安裝 (資料庫中)  
 下列範例顯示執行中的 R 服務的無訊息、 自動安裝時，在命令列中指定最小必要的功能 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  從提高權限的命令提示字元執行下列命令︰  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  安裝完成時，在之後 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，執行下列命令以啟用功能。  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  您必須明確啟用引擎功能，否則將無法叫用 R 指令碼，即使是安裝程式已安裝並設定此功能亦然。  
  
3.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 這也會自動重新啟動相關的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務。  
  
## 另請參閱  
 [R 服務安裝程式疑難排解](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  