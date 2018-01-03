---
title: "第 3 課：安裝 SSIS 套件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: adc1ce92302b10835ca88454b8a5f0bbdf179d50
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-3-install-ssis-packages"></a>第 3 課：安裝 SSIS 套件
在 [第 2 課：在 SSIS 中建立部署配套](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)中，您建立了部署公用程式，也建立了部署配套，其中包含您必須在其他電腦上安裝套件的項目。 此外，您也確認了部署配套中的檔案清單，並且檢查了建立部署公用程式時所建立的資訊清單檔內容。  
  
在這一課中，您會將部署配套複製到目的地電腦，然後執行「封裝安裝精靈」，將封裝、封裝相依性及輔助檔案安裝到該部電腦上。 套件將會安裝在 **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中，而其他項目則會安裝在檔案系統中。 完成封裝安裝之後，將會使用「執行封裝公用程式」從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行封裝，以測試部署。  
  
**完成本課程的估計時間** ：30 分鐘  
  
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：複製部署配套](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [步驟 2：執行封裝安裝精靈](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [步驟 3：測試部署的封裝](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製部署配套](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  
