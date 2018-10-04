---
title: XML 編輯器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.editorxml.f1
- sql12.swb.xmleditor.f1
- vs.xmleditor
- sql12.swb.editor.xml.f1
helpviewer_keywords:
- XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bf9af55c8ba7660a80dc65fa1f2eb6e322aad4f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166288"
---
# <a name="xml-editor-sql-server-management-studio"></a>XML 編輯器 (SQL Server Management Studio)
  提供一組視覺化工具，以搭配 XML 結構描述、ADO.NET 資料集以及 XML 文件使用。 XML 設計工具支援全球資訊網協會 (WC3) 定義的 XML 結構描述定義 (XSD) 語言。 設計師不支援 DTD (文件類型定義) 或其他 XML 結構描述語言，例如 XDR (XML-Data Reduced)。  
  
 若要顯示設計師，請在專案中加入資料集、XML 結構描述或 XML 檔案，或開啟下面資料表中所列出的任何檔案類型。  
  
> [!CAUTION]  
>  在結構描述檢視中作業時，沒有 **[恢復]** 命令可用。 請仔細規劃您的工作，並經常儲存檔案。  
  
 設計師提供下列三種檢視 (或模式) 來處理 XML 檔案、XML 結構描述和資料集：  
  
|檢視|描述|支援的檔案類型|  
|----------|-----------------|--------------------------|  
|**結構描述**|以視覺化的方式建立和修改 XML 結構描述與 ADO.NET 資料集。|.xsd|  
|**資料**|在結構化資料方格中，以視覺化的方式修改 XML 資料檔案。|.xml|  
|**XML**|用於編輯 XML；來源編輯器提供色彩編碼和 IntelliSense，其中包括自動完成和列出成員。|.xml .xsd .xslt .wsdl.web.resx.tdl.wsf.hta.disco.vsdisco.config|  
|**執行程序表**|顯示使用 SET SHOWPLAN_XML ON 選項建立的 xml 查詢計畫。|.showplan|  
  
## <a name="schema-view"></a>結構描述檢視  
 結構描述檢視提供元素、屬性、類型等等可組成 XML 結構描述和 ADO.NET 資料集的視覺表示法。  
  
 在結構描述檢視中，您可以從工具箱的 XML 結構描述索引標籤，或從伺服器總管，在設計介面上卸除元素，以建構結構描述和資料集。 此外，您可以用滑鼠右鍵按一下設計介面，或者從快速鍵功能表中選取 [加入]，以將元素加入設計師中。  
  
 在結構描述檢視中，您可以：  
  
-   建構並修改現有的 XML 結構描述和 ADO.NET 資料集  
  
-   建立與編輯資料表之間的關聯性  
  
-   建立與編輯索引鍵  
  
-   從 XML 結構描述產生 ADO.NET 資料集  
  
> [!NOTE]  
>  結構描述檢視中的元素配置儲存在 .xsx 檔案中，只要按一下方案總管工具列的 **[顯示所有檔案]** ，然後展開 .xsd 檔案就能看到。 如果沒有 .xsx 檔案，則表示從未於 XML 設計工具中開啟 .xsd 檔案。  
  
### <a name="customizing-schema-view"></a>自訂結構描述檢視  
 下列功能可以在結構描述檢視中修改元素的視覺化配置：  
  
-   顯示比例  
  
-   展開或摺疊巢狀元素  
  
-   自動排列元素配置  
  
-   重新設定摺疊元素的預設狀態  
  
##### <a name="to-expand-hidden-nested-elements"></a>若要展開隱藏的巢狀元素  
  
-   按一下元素底部的加號圖示。  
  
##### <a name="to-collapse-nested-elements"></a>若要摺疊巢狀元素  
  
-   在您要顯示於設計師的最底部元素上，按一下減號圖示。  
  
## <a name="data-view"></a>資料檢視  
 資料檢視提供資料方格，可以用來修改 .xml 檔案。 只有 XML 檔案中的內容 (但不包含標記和結構) 可以在資料檢視中編輯。  
  
 資料檢視中有兩個不同的區域： **[資料表]** 與 **[資料]**。 [資料表] 區域是 XML 檔案中定義的關聯清單，以巢狀結構為順序 (從最外層到最內層)。 **[資料]** 區域是資料方格，會根據資料表區域的選擇顯示資料。  
  
> [!NOTE]  
>  新建立的 XML 檔案中不包含資料，因此無法在資料檢視中顯示。 此外還有部份 XML文件的執行個體，其資料檢視完全無法叫用。 即使 XML 格式正確，但如果不是結構化資料卻嘗試切換到資料檢視，則會產生下列訊息：「雖然這份文件格式正確，但其中包含資料檢視無法顯示的結構。」  
  
 在資料檢視中，您可以：  
  
-   手動擴展資料表  
  
-   編輯現有的資料表  
  
-   自 XML 文件產生 XML 結構描述  
  
## <a name="xml-view"></a>XML 檢視  
 XML 檢視提供編輯器來編輯原始 XML，並提供 IntelliSense 和色彩編碼。 在處理具有相關聯之結構描述的 .xsd 檔案與 .xml 檔案時，可以使用陳述式完成。 型別\<起始標記，就會看到一份在該位置是有效的項目。 鍵入元素名稱並按下空格鍵之後，將會出現該元素所支援的屬性清單。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 選項。 在 XML 編輯器中，若要存取選項，請在 **[編輯]** 功能表上，按一下 **[IntelliSense]**。  
  
## <a name="showplan-view"></a>SHOWPLAN 檢視  
 查詢計畫使用 SET SHOWPLAN_XML ON 選項建立時，就可以將查詢計畫以 XML 格式儲存。 在副檔名為 .showplan 的檔案上按兩下，即可開啟查詢計畫。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式儲存執行計畫](../performance/save-an-execution-plan-in-xml-format.md)  
  
  
