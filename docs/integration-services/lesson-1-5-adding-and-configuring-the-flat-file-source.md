---
title: 步驟 5：加入和設定一般檔案來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 996c74d9810464c1da294343d4deb1bf5fe1dd8e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-5---adding-and-configuring-the-flat-file-source"></a>課程 1-5 - 加入和設定一般檔案來源
在這項工作中，您會在封裝中加入和設定一般檔案來源。 一般檔案來源是一個資料流程元件，它使用一般檔案連接管理員所定義的中繼資料，來指定轉換處理序要從一般檔案擷取之資料的格式和結構。 一般檔案來源可設定為使用一般檔案連接管理員提供的檔案格式定義，從單個一般檔案擷取資料。  
  
在此教學課程中，您將設定一般檔案來源使用您先前建立的 **[範例一般檔案來源資料]** 連接管理員。  
  
### <a name="to-add-a-flat-file-source-component"></a>若要加入一般檔案來源元件  
  
1.  按兩下 [擷取範例貨幣資料] 資料流程工作，或按一下 [資料流程] 索引標籤，來開啟 [資料流程] 設計師。  
  
2.  在 [SSIS 工具箱] 中，展開 [其他來源]，然後將 [一般檔案來源] 拖曳至 [資料流程] 索引標籤的設計介面中。  
  
3.  在 [資料流程] 設計介面中，以滑鼠右鍵按一下新加入的 [一般檔案來源]，按一下 [重新命名]，將名稱變更為**擷取範例貨幣資料**。  
  
4.  按兩下一般檔案來源，來開啟 [一般檔案來源編輯器] 對話方塊。  
  
5.  在 **[一般檔案連接管理員]** 方塊中，選取 **範例一般檔案來源資料**。  
  
6.  按一下 **[資料行]** 並確認資料行的名稱正確無誤。  
  
7.  按一下 [確定] 。  
  
8.  以滑鼠右鍵按一下一般檔案來源，然後按一下 **[屬性]**。  
  
9. 在 [屬性] 視窗中，確認 **LocaleID** 屬性是設為 **[英文 (美國)]**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 6：加入及設定查閱轉換](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>另請參閱  
[一般檔案來源](../integration-services/data-flow/flat-file-source.md)  
[一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
