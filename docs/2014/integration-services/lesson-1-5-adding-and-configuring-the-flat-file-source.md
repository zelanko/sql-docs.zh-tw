---
title: 步驟 5：新增和設定一般檔案來源 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bfca1c78bdc0c11b3aac18bf6e6b0b2b0344b109
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815210"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>步驟 5：加入和設定一般檔案來源
  在這項工作中，您會在封裝中加入和設定一般檔案來源。 一般檔案來源是一個資料流程元件，它使用一般檔案連接管理員所定義的中繼資料，來指定轉換處理序要從一般檔案擷取之資料的格式和結構。 一般檔案來源可設定為使用一般檔案連接管理員提供的檔案格式定義，從單個一般檔案擷取資料。  
  
 本教學課程中，您將設定要使用的一般檔案來源`Sample Flat File Source Data`您先前建立的連接管理員。  
  
### <a name="to-add-a-flat-file-source-component"></a>若要加入一般檔案來源元件  
  
1.  開啟**資料流程**設計工具中，按兩下`Extract Sample Currency Data`資料流程工作，或按一下 **資料流程索引標籤**。  
  
2.  在 [SSIS 工具箱] 中，展開 [其他來源]，然後將 [一般檔案來源] 拖曳至 [資料流程] 索引標籤的設計介面中。  
  
3.  在上**資料流程**設計介面上，以滑鼠右鍵按一下 新增**一般檔案來源**，按一下 **重新命名**，並將名稱變更為`Extract Sample Currency Data`。  
  
4.  按兩下一般檔案來源，來開啟 [一般檔案來源編輯器] 對話方塊。  
  
5.  在 **一般檔案連接管理員**方塊中，選取`Sample Flat File Source Data`。  
  
6.  按一下 **[資料行]** 並確認資料行的名稱正確無誤。  
  
7.  按一下 [確定] 。  
  
8.  以滑鼠右鍵按一下一般檔案來源，然後按一下 **[屬性]**。  
  
9. 在 [屬性] 視窗中，確認`LocaleID`屬性設定為**英文 （美國）**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 6:加入及設定查閱轉換](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>另請參閱  
 [一般檔案來源](data-flow/flat-file-source.md)   
 [一般檔案連線管理員編輯器 &#40;[一般]頁面&#41;](general-page-of-integration-services-designers-options.md)  
  
  
