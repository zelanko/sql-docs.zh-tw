---
title: 第 5 課：新增套件部署模型的 SSIS 套件設定 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3b3ccea56d367e7870826b39830e415e26bb2ac
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295904"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>第 5 課：新增套件部署模型的 SSIS 套件設定

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



套件設定可讓您從開發環境之外設定執行階段屬性和變數。 組態可讓您開發彈性且易於部署和散發的封裝。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會提供下列組態類型：  
  
-   XML 組態檔  
  
-   環境變數  
  
-   登錄項目  
  
-   父封裝變數  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表  
  
在本課程中，您會修改範例 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件，這是您在[第 4 課：使用 SSIS 新增錯誤流程重新導向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)中建立的套件，以便使用套件部署模型並利用套件設定。 您也可以複製隨附於此教學課程中已完成的第 4 課套件。 

使用 [套件設定精靈]，建立 XML 設定來更新 Foreach 迴圈容器的 **Directory** 屬性。 您會使用對應至 **Directory** 屬性的套件層級變數。 建立設定檔之後，您可以從開發環境之外，將變數的值修改為新的範例資料夾路徑。 當您再次執行封裝時，設定檔會填入該變數的值，然後由該變數更新 **Directory** 屬性。 套件接著會反覆執行新資料夾中的檔案，而不是原始硬式編碼資料夾中的檔案。  
  
> [!NOTE]
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。
  
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：複製第 4 課套件](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [步驟 2：啟用和設定套件設定](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [步驟 3：修改 Directory 屬性設定值](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [步驟 4：測試第 5 課套件](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
  
-   [步驟 1：複製第 4 課套件](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
