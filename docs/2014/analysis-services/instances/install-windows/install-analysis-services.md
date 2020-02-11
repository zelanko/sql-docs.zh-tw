---
title: 以表格式模式安裝 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bf1a8ee0d5dd3dde585a027fd08fd833fb40304
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079905"
---
# <a name="install-analysis-services-in-tabular-mode"></a>以表格模式安裝 Analysis Services
  如果您安裝 Analysis Services 以使用新表格式模型功能，則必須在支援該模型類型的伺服器模式下安裝 Analysis Services。 此伺服器模式為表格式，並會在安裝期間設定。  
  
 在此模式下安裝伺服器之後，即可用來裝載您在表格式模型設計師中建立的方案。 如果您想透過網路存取表格式模型資料，則需要表格模式伺服器。  
  
 您可以在 [安裝精靈] 或命令列安裝程式中指定表格模式。 下列各節將描述各種方法。  
  
## <a name="installation-wizard"></a>安裝精靈  
 下列清單顯示 [SQL Server 安裝精靈] 中，用來在表格模式下安裝 Analysis Services 的頁面：  
  
1.  從安裝程式的 [功能樹狀目錄] 中，選取 **[Analysis Services]** 。  
  
     ![顯示 Analsyis Services 的安裝功能樹狀結構](../../../sql-server/install/media/ssas-setupas.gif "顯示 Analsyis Services 的安裝功能樹狀結構")  
  
2.  在 [Analysis Services 設定] 頁面上，請務必選取 [**表格式模式]**。  
  
     ![Analysis Services 組態選項中的安裝頁面](../../../sql-server/install/media/ssas-setupasconfig.gif "Analysis Services 組態選項中的安裝頁面")  
  
 表格模式使用 xVelocity 記憶體中分析引擎 (VertiPaq)，這是您部署至 Analysis Services 之表格式模型的預設儲存引擎。 將表格式模型方案部署至伺服器之後，您可以選擇設定表格式方案，以使用 DirectQuery 磁碟儲存體作為記憶體繫結之儲存引擎的替代儲存體。  
  
## <a name="command-line-setup"></a>命令列安裝程式  
 SQL Server 安裝程式包含可指定伺服器模式的新參數 (`ASSERVERMODE`)。 下列範例說明在表格式伺服器模式下安裝 Analysis Services 的命令列安裝程式。  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 
  `INSTANCENAME` 必須少於 17 個字元。  
  
 所有預留位置帳戶值都必須取代成有效的帳戶和密碼。  
  
 使用所提供的範例命令列語法時，不會安裝 SQL Server Management Studio 或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 之類的工具。 如需新增功能的詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
 
  `ASSERVERMODE` 會區分大小寫。  所有值都必須以大寫形式表示。 下表描述 `ASSERVERMODE` 的有效值。  
  
|值|描述|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|這是預設值。 如果您未設定 `ASSERVERMODE`，伺服器會以多維度伺服器模式安裝。|  
|POWERPIVOT|此為選用值。 實際上，如果您設定 `ROLE` 參數，即會自動將伺服器模式設為 1，使得 `ASSERVERMODE` 成為 PowerPivot for SharePoint 安裝的選用參數。 如需詳細資訊，請參閱[從命令提示字元安裝 PowerPivot](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md)。|  
|TABULAR|如果您使用命令列安裝程式，在表格模式下安裝 Analysis Services，則需要此值。|  
  
## <a name="see-also"></a>另請參閱  
 [判斷 Analysis Services 實例的伺服器模式](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [設定表格式模型資料庫的記憶體內部或 DirectQuery 存取](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [&#40;SSAS 表格式&#41;的表格式模型](../../tabular-models/tabular-models-ssas.md)  
  
  
