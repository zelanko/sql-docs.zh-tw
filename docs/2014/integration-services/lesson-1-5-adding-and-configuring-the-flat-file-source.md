---
title: 步驟 5：加入和設定一般檔案來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32b95a5d156ae52394b7128b024c86b9a7e308b1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62891536"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>步驟 5：新增和設定一般檔案來源
  在這項工作中，您會在封裝中加入和設定一般檔案來源。 一般檔案來源是一個資料流程元件，它使用一般檔案連接管理員所定義的中繼資料，來指定轉換處理序要從一般檔案擷取之資料的格式和結構。 一般檔案來源可設定為使用一般檔案連接管理員提供的檔案格式定義，從單個一般檔案擷取資料。  
  
 在本教學課程中，您會將一般檔案來源設定為`Sample Flat File Source Data`使用您先前建立的連接管理員。  
  
### <a name="to-add-a-flat-file-source-component"></a>若要加入一般檔案來源元件  
  
1.  按兩下 [**資料流程**] 工作`Extract Sample Currency Data` ，或按一下 [**資料流程]** 索引標籤，以開啟 [資料流程設計師]。  
  
2.  在 [SSIS 工具箱]**** 中，展開 [其他來源]****，然後將 [一般檔案來源]**** 拖曳至 [資料流程]**** 索引標籤的設計介面中。  
  
3.  在 [**資料流程] 設計介面**上，以滑鼠右鍵按一下新加入的 [一般檔案**來源**]，按一下 [**重新命名**]，然後將名稱變更為`Extract Sample Currency Data`。  
  
4.  按兩下一般檔案來源，來開啟 [一般檔案來源編輯器] 對話方塊。  
  
5.  在 [一般檔案**連接管理員**] 方塊中`Sample Flat File Source Data`，選取 []。  
  
6.  按一下 **[資料行]** 並確認資料行的名稱正確無誤。  
  
7.  按一下 [確定]  。  
  
8.  以滑鼠右鍵按一下一般檔案來源，然後按一下 **[屬性]**。  
  
9. 在 [屬性視窗中，確認屬性`LocaleID`是設為 [**英文（美國）**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 6：新增和設定查閱轉換](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>另請參閱  
 [一般檔案來源](data-flow/flat-file-source.md)   
 [一般檔案連線管理員編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)  
  
  
