---
title: 步驟 1:複製部署配套 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 153975d4b2a418c694188ca30c0ddb9fc19b0fc8
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722391"
---
# <a name="lesson-3-1---copying-the-deployment-bundle"></a>課程 3-1 - 複製部署配套

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


在這項工作中，您會將部署配套複製到目的地電腦。  
  
要將部署配套複製到目的地電腦，最簡單的方式就是先在目的地電腦上建立一個公用共用區，再將磁碟機對應至此公用共用區，然後將部署配套複製到此共用區。 如果不知道如何建立和設定公用資料夾或對應磁碟機，請參閱 Windows 文件集。  
  
### <a name="to-copy-the-deployment-bundle"></a>若要複製部署配套  
  
1.  在電腦上找到部署配套。  
  
    如果使用的是預設位置，則部署配套就是 [部署教學課程] 資料夾內的 Bin\Deployment 資料夾。  
  
2.  以滑鼠右鍵按一下 [Deployment] 資料夾，然後按一下 [複製]。  
  
3.  在目標電腦上找到您要複製此資料夾的公用共用，然後按一下 [貼上]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 2：執行套件安裝精靈](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
  
  
