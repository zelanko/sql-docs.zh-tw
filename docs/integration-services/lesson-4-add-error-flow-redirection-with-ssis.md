---
title: 第 4 課：使用 SSIS 來新增錯誤流程重新導向 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8858494792a8acd9d1af7aee887c24e45d8829f9
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918123"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>第 4 課：使用 SSIS 來新增錯誤流程重新導向

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



為了處理可能在轉換過程中發生的錯誤，[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可讓您針對每個元件和每個資料行，決定要如何處理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 無法轉換的資料。 您可以選擇忽略特定資料行的失敗、將整個失敗的資料列重新導向，或讓該元件失敗。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的元件預設是設定為在發生錯誤時失敗。 失敗的元件會進而造成套件失敗，接著處理就會停止。  
  
您可以設定和處理可能發生的處理錯誤，而不要讓失敗停止套件執行。 其中一個選項是忽略全部失敗，讓您的套件一律執行成功。 您也可以將失敗的資料列重新導向到另一個處理路徑，以便在該處保存、檢查或重新處理資料和錯誤。  
  
在本課程中，您會為在[第 3 課：使用 SSIS 新增記錄功能](../integration-services/lesson-3-add-logging-with-ssis.md)中開發的套件建立一個複本。 您將利用這個新的套件，建立其中一個範例資料檔的損毀版本。 當您執行套件時，損毀的檔案會導致發生處理錯誤。  
  
為了處理錯誤資料，您需新增及設定可將任何失敗資料列寫入錯誤檔的「一般檔案」目的地。 
  
在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 將錯誤資料寫入檔案之前，您需併入一個會取得錯誤描述的「指令碼」元件。 然後，您需重新設定 [查閱貨幣索引鍵] 轉換，以將任何無法處理的資料重新導向到 [指令碼] 轉換。  
  
## <a name="prerequisites"></a>Prerequisites

> [!NOTE]
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。
 
## <a name="lesson-task"></a>課程工作
這一課包含下列工作：  
  
-   [步驟 1：複製第 3 課套件](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [步驟 2：建立損毀的檔案](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [步驟 3：新增錯誤流程重新導向](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [步驟 4：新增一般檔案目的地](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [步驟 5：測試第 4 課教學課程套件](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製第 3 課套件](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
