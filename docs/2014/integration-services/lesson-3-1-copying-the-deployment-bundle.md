---
title: 步驟 1:複製部署配套 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d28a85e4dccaa6165d96046848513879998136f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891707"
---
# <a name="step-1-copying-the-deployment-bundle"></a>步驟 1:複製部署配套
  在這項工作中，您會將部署配套複製到目的地電腦。  
  
 要將部署配套複製到目的地電腦，最簡單的方式就是先在目的地電腦上建立一個公用共用區，再將磁碟機對應至此公用共用區，然後將部署配套複製到此共用區。 如果不知道如何建立和設定公用資料夾或對應磁碟機，請參閱 Windows 文件集。  
  
### <a name="to-copy-the-deployment-bundle"></a>若要複製部署配套  
  
1.  在電腦上找到部署配套。  
  
     如果使用的是預設位置，則部署配套就是 [部署教學課程] 資料夾內的 Bin\Deployment 資料夾。  
  
2.  以滑鼠右鍵按一下 [Deployment] 資料夾，然後按一下 [複製]。  
  
3.  在目標電腦上找到您要複製此資料夾的公用共用，然後按一下 [貼上]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2：執行套件安裝精靈](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
