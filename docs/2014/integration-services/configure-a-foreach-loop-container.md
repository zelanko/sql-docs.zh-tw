---
title: 設定 Foreach 迴圈容器 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
caps.latest.revision: 36
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6eb60b4292ac3357ea2e2fcc27a6a36ae4bea608
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298768"
---
# <a name="configure-a-foreach-loop-container"></a>設定 Foreach 迴圈容器
  此程序描述如何設定「Foreach 迴圈」容器，包括列舉值及容器層級的屬性運算式。  
  
### <a name="to-configure-the-foreach-loop-container"></a>設定 Foreach 迴圈容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  按一下 [控制流程] 索引標籤，然後按兩下 [Foreach 迴圈]。  
  
3.  在 [Foreach 迴圈編輯器] 對話方塊中，按一下 [一般]，然後選擇性地修改 [Foreach 迴圈] 的名稱及描述。  
  
4.  按一下 [集合]從 [列舉值] 清單選取列舉值類型。  
  
5.  指定列舉值並設定列舉值選項如下：  
  
    -   若要使用 Foreach 檔案列舉值，請提供包含要列舉之檔案的資料夾，指定檔案名稱及類型的篩選，並指定是否應該傳回完整的檔案名稱。 同時，指示是否遞迴所有子資料夾，以取得更多檔案。  
  
    -   若要使用 Foreach 項目列舉值，請按一下 [資料行]，然後在 [For Each 項目資料行] 對話方塊中，按一下 [加入]以加入資料行。 在 [資料類型] 清單中為每個資料行選取資料類型，然後按一下 [確定]。  
  
         在資料行中鍵入值，或從清單選取值。  
  
        > [!NOTE]  
        >  若要加入新的資料列，請按一下您鍵入項目之資料格以外的任何位置。  
  
        > [!NOTE]  
        >  如果值與資料行資料類型不相容，則文字會反白顯示。  
  
    -   若要使用 Foreach ADO 列舉值，請選取現有的變數，或按一下 [ADO 物件來源變數] 清單中的 [新增變數]，以指定包含要列舉之 ADO 物件名稱的變數，然後選取列舉模式選項。  
  
         如果要建立新變數，請在 [加入變數] 對話方塊中設定變數屬性。  
  
    -   若要使用 Foreach ADO.NET 結構描述資料列集列舉值，請選取現有的 ADO.NET 連接，或按一下 [連接] 清單中的 [新增連接]，然後選取結構描述。  
  
         您可選擇按一下 [設定限制] 並選取結構描述限制，再選取包含限制值的變數或輸入限制值，然後按一下 [確定]。  
  
    -   若要使用 Foreach From Variable 列舉值，請在 [變數] 清單中選取變數。  
  
    -   若要使用 Foreach NodeList 列舉值，請按一下 [DocumentSourceType] 並從清單中選取來源類型，然後按一下 [DocumentSource]。 視 DocumentSourceType 所選的值而定，從清單中選取變數或檔案連接、建立新的變數或檔案連接，或在 [文件來源編輯器] 中輸入 XML 來源。  
  
         接著，按一下 [EnumerationType] 並從清單中選取列舉類型。 如果 EnumerationType 是 **Navigator、Node 或 NodeText**，請按一下 [OuterXPathStringSourceType] 並選取來源類型，然後按一下 [OuterXPathString]。 視 OuterXPathStringSourceType 所設定的值而定，從清單中選取變數或檔案連接、建立新的變數或檔案連接，或為外部 XML 路徑語言 (XPath) 運算式輸入字串。  
  
         如果 EnumerationType 是 **ElementCollection**，請如上所述設定 OuterXPathStringSourceType 和 OuterXPathString。 然後，按一下 [InnerElementType] 並為內部元素選取列舉類型，再按一下 [InnerXPathStringSourceType]。 視 InnerXPathStringSourceType 所設定的值而定，選取變數或檔案連接、建立新的變數或檔案連接，或為內部 XPath 運算式輸入字串。  
  
    -   若要使用 Foreach SMO 列舉值，請選取現有的 ADO.NET 連接，或按一下 [連接] 清單中的 [新增連接]，然後輸入要使用的字串或按一下 [瀏覽]。 如果按一下 [選取 SMO 列舉] 對話方塊中的 [瀏覽]，請選取要列舉的物件類型及列舉類型，然後按一下 [確定]。  
  
6.  (選擇性) 按一下 [集合] 頁面上 [運算式] 文字方塊中的瀏覽按鈕 **(…)**，以建立更新屬性值的運算式。 如需詳細資訊，請參閱[加入或變更屬性運算式](expressions/add-or-change-a-property-expression.md)。  
  
    > [!NOTE]  
    >  [屬性] 清單中列出的屬性會依列舉值而不同。  
  
7.  (選擇性) 按一下 [變數對應]，以將物件屬性對應至集合值，然後執行下列操作：  
  
    1.  在 [變數] 清單中選取變數，或按一下 [\<新增變數>]，以建立新的變數。  
  
    2.  如果您加入新的變數，請在 [加入變數] 對話方塊中設定變數屬性，然後按一下 [確定]。  
  
    3.  如果您使用 ForEach 項目列舉值，則可以在 [索引] 清單中更新索引值。  
  
        > [!NOTE]  
        >  索引值指示項目中要對應至變數的資料行。 只有「For Each 項目」列舉值可以使用 0 之外的索引值。  
  
8.  (選擇性) 按一下 [運算式] 頁面上的 [運算式]，建立 Foreach 迴圈容器之屬性的屬性運算式。 如需詳細資訊，請參閱[加入或變更屬性運算式](expressions/add-or-change-a-property-expression.md)。  
  
9. 按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
 [Foreach 迴圈容器](control-flow/foreach-loop-container.md)  
  
  
