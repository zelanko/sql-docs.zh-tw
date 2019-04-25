---
title: 第 3 課：安裝套件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da763e2385c64a09279c9dd6ff537993c2cd6a30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767570"
---
# <a name="lesson-3-installing-packages"></a>第 3 課：安裝封裝
  在[第 2 課：建立部署配套](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)，您建立了部署公用程式，也建立了部署配套所包含的項目，您必須在另一部電腦上安裝封裝。 此外，您也確認了部署配套中的檔案清單，並且檢查了建立部署公用程式時所建立的資訊清單檔內容。  
  
 在這一課中，您會將部署配套複製到目的地電腦，然後執行「封裝安裝精靈」，將封裝、封裝相依性及輔助檔案安裝到該部電腦上。 套件將會安裝在 **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中，而其他項目則會安裝在檔案系統中。 完成封裝安裝之後，將會使用「執行封裝公用程式」從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行封裝，以測試部署。  
  
 **完成本課程的估計時間：** 30 分鐘  
  
## <a name="lesson-tasks"></a>課程工作  
 這一課包含下列工作：  
  
-   [步驟 1：複製部署配套](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [步驟 2：執行套件安裝精靈](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [步驟 3：測試部署的套件](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>開始課程  
 [步驟 1：複製部署配套](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
