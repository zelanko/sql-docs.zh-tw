---
title: Integration Services （SSIS）和 Studio 環境 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ef53f08f457d9122b1ab965d0269717379779335
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965424"
---
# <a name="integration-services-ssis-and-studio-environments"></a>Integration Services (SSIS) 和 Studio 環境
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含兩個可搭配 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]使用的 Studio：  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 可用於開發商務解決方案所需的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會提供 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，讓您在其中建立封裝。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 適合用來在實際執行環境中管理套件。  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]在  中工作時，您可以執行下列工作：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行 [ 匯入和匯出精靈]，以便建立將資料從來源複製至目的地的基本封裝。  
  
-   建立包含複雜控制流程、資料流程、事件驅動邏輯及記錄的封裝。  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] 使用「 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]設計師」中的疑難排解及監視功能與  中的偵錯功能，對封裝進行測試及偵錯。  
  
-   建立在執行階段更新封裝及封裝物件之屬性的組態。  
  
-   建立可在其他電腦上安裝封裝及其相依性的部署公用程式。  
  
-   將封裝的複本儲存至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 資料庫、[!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區及檔案系統。  
  
 如需 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的詳細資訊，請參閱 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/hh272686.aspx)。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會提供 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，您可以使用該服務管理封裝、監視執行中封裝以及判斷 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的影響及資料歷程。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]在  中工作時，您可以執行下列工作：  
  
-   建立資料夾，以便使用對您的組織具有意義的方式組織封裝。  
  
-   使用「執行封裝」公用程式，執行儲存在本機電腦上的封裝。  
  
-   執行「執行封裝」公用程式產生執行 **dtexec** 命令提示字元公用程式 (dtexec.exe) 時使用的命令列。  
  
-   將封裝匯入和匯出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 資料庫、「[!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區」及檔案系統。  
  
