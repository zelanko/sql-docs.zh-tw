---
title: 第 2 課：使用 SSIS 來新增迴圈 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e8903517affd4d0a8e395a17cb97e27ddd5a67d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65722448"
---
# <a name="lesson-2-add-looping-with-ssis"></a>第 2 課：使用 SSIS 來新增迴圈

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在[第 1 課：使用 SSIS 建立專案和基本套件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)中，您已建立會從單一一般檔案來源擷取資料的套件。 接著，套件會使用「查閱」轉換來轉換該資料。 最後，套件會將資料載入至 **AdventureWorksDW2012** 範例資料庫的 **FactCurrencyRate** 事實資料表複本中。  
  
「擷取、轉換和載入」(ETL) 程序通常會從多個一般檔案來源擷取資料。 從多個來源擷取資料需要反覆的控制流程。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可以輕鬆地將反覆運算或迴圈新增到套件中。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供兩種類型的容器來循環使用封裝迴圈：Foreach 迴圈容器和 For 迴圈容器。 雖然「Foreach 迴圈」容器通常使用變數運算式，但「Foreach 迴圈」容器會使用列舉值來執行迴圈。 這一課使用 Foreach 迴圈容器。  
  
Foreach 迴圈容器可讓封裝對指定列舉值的每一位成員重複控制流程。 利用 Foreach 迴圈容器，您可以列舉：  
  
-   ADO 記錄集資料列  
  
-   ADO .Net 結構描述資訊  
  
-   檔案和目錄結構  
  
-   系統、套件及使用者變數  
  
-   變數中的可列舉物件  
  
-   集合中的項目  
  
-   XML 路徑語言 (XPath) 運算式中的節點  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件 (SMO)  
  
在本課程中，您會將第 1 課的範例 ETL 套件修改成使用「Foreach 迴圈」容器，並為套件設定使用者定義的套件變數。 該變數會接著用來逐一查看範例資料夾中相符的檔案。   
  
在本課程中，您不會修改資料流程，只會修改控制流程。  
  
> [!NOTE]  
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。

## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
-   [步驟 1：複製第 1 課套件](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [步驟 2：新增及設定 Foreach 迴圈容器](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [步驟 3：修改一般檔案連線管理員](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [步驟 4：測試第 2 課教學課程套件](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製第 1 課套件](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>另請參閱  
[For 迴圈容器](../integration-services/control-flow/for-loop-container.md)  
  
  
  
