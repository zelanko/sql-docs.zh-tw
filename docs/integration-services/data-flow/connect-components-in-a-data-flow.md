---
title: "連接資料流程中的元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 73a379b190f05f4eedc361b4557afefd700a9664
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="connect-components-in-a-data-flow"></a>連接資料流程中的元件
  此程序描述如何將資料流程中的元件輸出，連接到同一資料流程中的其他元件。  
您可以在 **設計師中** [資料流程] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 索引標籤的設計介面上，建構封裝中的資料流程。 如果資料流程包含兩個資料流程元件，將來源或轉換的輸出連接到轉換或目的地的輸入，便可以連接這兩個元件。 兩個資料流程元件之間的連接子稱為路徑。  
  
 下圖顯示的範例資料流程中，包含一個來源元件、兩個轉換、一個目的地元件，以及連接元件的路徑。  
  
 ![Data flow](../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 在連接兩個元件之後，您可以在 **[資料流程路徑編輯器]**中，檢視經由路徑移動的資料之中繼資料，以及路徑的屬性。 如需詳細資訊，請參閱 [Integration Services Paths](../../integration-services/data-flow/integration-services-paths.md)。  
  
 您也可以將資料檢視器加入路徑。 資料檢視器可讓您在封裝執行時，檢視在資料流程元件之間移動的資料。  
  
### <a name="connect-components-in-a-data-flow"></a>連接資料流程中的元件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含您要在其中連接元件之資料流程的「資料流程」工作。  
  
4.  在 [資料流程] 索引標籤的設計介面上，選取您要連接的轉換或來源。  
  
5.  將轉換或來源的綠色輸出箭頭拖曳至另一轉換或目的地。 某些資料流程元件有錯誤輸出，您可以使用相同方式加以連接。  
  
    > [!NOTE]  
    >  某些資料流程元件具有多個輸出，您可以將每個輸出連接到另一個轉換或目的地。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [在資料流程中加入或刪除元件](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [偵錯資料流程](../../integration-services/troubleshooting/debugging-data-flow.md)[資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
