---
title: 第 5 課：加入封裝部署模型的 SSIS 封裝組態 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 079c271a7f9cb2f33c90fb8c4b0914319ea190f8
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331912"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>第 5 課：加入套件部署模型的 SSIS 套件組態
封裝組態可讓您從開發環境之外設定執行階段屬性和變數。 組態可讓您開發彈性且易於部署和散發的封裝。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會提供下列組態類型：  
  
-   XML 組態檔  
  
-   環境變數  
  
-   登錄項目  
  
-   父封裝變數  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] table  
  
在本課程中，您將修改在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 第 4 課：使用 SSIS 加入錯誤流程重新導向 [中建立的簡單](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) 套件，以便使用套件部署模型並利用套件組態。 您也可以複製此教學課程所包含之已完成的第 4 課封裝。 您可以使用封裝組態精靈，建立一個 XML 組態，以利用一個對應至 **Directory** 屬性的套件層級變數，來更新 Foreach 迴圈容器的 Directory 屬性。 建立組態檔之後，您可以從開發環境之外修改變數的值，並將已修改的屬性指向新的範例資料夾。 當您再次執行套件時，設定檔會填入該變數的值，然後由該變數更新 **Directory**屬性。 因此，封裝會反覆執行新儲存資料的資料夾之檔案，而不反覆執行以寫入程式碼的方式寫入封裝內之原始資料夾的檔案。  
  
> [!IMPORTANT]  
> 這個教學課程需要 **AdventureWorksDW2012** 範例資料庫。 如需如何安裝和部署 **AdventureWorksDW2012**的詳細資訊，請參閱 [CodePlex 上的 Reporting Services 產品範例](http://go.microsoft.com/fwlink/p/?LinkID=526910)。  
  
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：複製第 4 課的套件](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [步驟 2：啟用和設定封裝組態](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [步驟 3：修改 Directory 屬性組態值](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [步驟 4：測試第 5 課的教學課程封裝](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
  
-   [步驟 1：複製第 4 課的套件](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
