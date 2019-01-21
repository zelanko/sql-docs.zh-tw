---
title: 第 3 課：使用 SSIS 來新增記錄功能 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 790738d3c66d4b973d2f6934e89caa77af6ffde0
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54142998"
---
# <a name="lesson-3-add-logging-with-ssis"></a>第 3 課：使用 SSIS 來新增記錄功能

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供工作和容器事件的追蹤，包含可讓您進行疑難排解及監視套件執行的記錄功能。 記錄功能是具有彈性的。 您可以在套件層級啟用記錄功能，也可以在套件內的個別工作或容器上啟用記錄功能。 您可以選取要記錄哪些事件，以及針對單一套件建立多個記錄。  
  
記錄提供者會建立記錄。 每一個記錄提供者都可將記錄資訊寫入至不同格式和目的地類型。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供下列記錄提供者：  
  
-   文字檔  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 事件記錄檔  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 檔  
  
在本課程中，您會建立您在[第 2 課：使用 SSIS 來新增迴圈](../integration-services/lesson-2-adding-looping-with-ssis.md)中所建立套件的複本。 使用這個新套件時，您需接著新增及設定記錄功能，以在套件執行期間監視特定的事件。 如果您尚未完成前面任何一課，則也可以複製本教學課程隨附之已完成的第 2 課套件。  

> [!NOTE]
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。

## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：複製第 2 課套件](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [步驟 2：新增及設定記錄](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [步驟 3：測試第 3 課套件](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製第 2 課套件](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
