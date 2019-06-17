---
title: 使用 XML 來源來擷取資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c7a9b107a05b0645f2286f534f457d46a1b6f11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771094"
---
# <a name="extract-data-by-using-the-xml-source"></a>使用 XML 來源來擷取資料
  若要加入和設定 XML 來源，封裝必須至少含有一個「資料流程」工作。  
  
### <a name="to-extract-data-using-an-xml-source"></a>使用 XML 來源擷取資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [資料流程]  索引標籤，然後將 XML 來源從 [工具箱]  拖曳至設計介面。  
  
4.  按兩下 XML 來源。  
  
5.  在 [XML 來源編輯器]  的 [連線管理員]  頁面上，選取資料存取模式：  
  
    -   若為 [XML 檔案位置]  存取模式，請按一下 [瀏覽]  ，以尋找包含 XML 檔案的資料夾。  
  
    -   若為 [來自變數的 XML 檔案]  存取模式，請選取包含 XML 檔案路徑的使用者定義變數。  
  
    -   若為 [來自變數的 XML 資料]  存取模式，請選取包含 XML 資料的使用者定義變數。  
  
    > [!NOTE]  
    >  變數必須定義於包含 XML 來源之「資料流程」工作的範圍內，或定義於封裝的範圍內；此外，變數還必須具有字串資料類型。  
  
6.  (選擇性) 選取 [使用內嵌結構描述]  ，來指示 XML 文件包含結構描述資訊。  
  
7.  若要指定 XML 檔案的外部「XML 結構描述定義語言」(XSD) 結構描述，請執行下列其中之一：  
  
    -   按一下 [瀏覽]  ，以尋找現有 XSD 檔案。  
  
    -   按一下 [產生 XSD]  ，以從 XML 檔案建立 XSD。  
  
8.  若要更新輸出資料行的名稱，請按一下 [資料行]  ，然後編輯 [輸出資料行]  清單中的值。  
  
9. 若要設定錯誤輸出，請按一下 **[錯誤輸出]** 。 如需詳細資訊，請參閱 [在資料流程元件中設定錯誤輸出](../configure-an-error-output-in-a-data-flow-component.md)。  
  
10. 按一下 [確定]  。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [XML 來源](xml-source.md)   
 [Integration Services 轉換](transformations/integration-services-transformations.md)   
 [Integration Services 路徑](integration-services-paths.md)   
 [資料流程工作](../control-flow/data-flow-task.md)  
  
  
