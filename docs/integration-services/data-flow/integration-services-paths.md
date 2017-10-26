---
title: "Integration Services 路徑 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 541c8faa4c878922411680646f3fa7a557eefe0f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-paths"></a>Integration Services 路徑
  將一個資料流程元件的輸出與另一元件的輸入連接，路徑可連接資料流程中的兩個元件。 路徑具有一個來源和一個目的地。 例如，如果路徑連接 OLE DB 來源和「排序」轉換，則 OLE DB 來源是路徑的來源，而「排序」轉換是路徑的目的地。 來源是路徑開始處的元件，而目的地是路徑結束處的元件。  
  
 如果您在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中執行封裝，則可將資料檢視器附加到路徑，來檢視資料流程中的資料。 資料檢視器可以設定為在方格中顯示資料。 資料檢視器是一種有用的偵錯工具。 如需詳細資訊，請參閱 [偵錯資料流程](../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
## <a name="configure-the-path"></a>設定路徑  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師提供 [資料流程路徑編輯器] 對話方塊，用以設定路徑屬性、檢視通過該路徑之資料行的中繼資料，並設定資料檢視器。  
  
 可設定的路徑屬性包括名稱、描述及路徑的註解。 您還可以程式設計方式設定路徑。 如需詳細資訊，請參閱[以程式設計方式連接資料流程元件](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)。  
  
 路徑註解顯示路徑來源的名稱，或在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中 [資料流程] 索引標籤設計介面上的路徑名稱。 路徑註解與您可加入資料流程、控制流程和事件處理常式的註解相似。 唯一不同之處在於路徑註解是附加到路徑上的，而其他註解則顯示於 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [資料流程]、[控制流程] 和 [事件處理常式] 索引標籤上。  
  
 中繼資料顯示上一個元件輸出中之每個資料行的名稱、資料類型、有效位數、小數位數、長度、字碼頁和來源元件。 來源元件是建立資料行的資料流程元件。 但不一定是資料流程中的第一個元件。 例如，「聯集全部」和「排序」轉換都會建立自己的資料行，因此它們是其輸出資料行的來源。 相反地，「複製資料行」轉換可以通過資料行而不對其進行變更，或可以藉由複製輸入資料行來建立新的資料行。 因此「複製資料行」轉換僅是新資料行的來源元件。  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>設定路徑以資料流程路徑編輯器 的屬性
路徑會連接兩個資料流程元件。 在您可以設定路徑屬性之前，資料流程必須包含至少兩個已連接的資料流程元件。
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [資料流程] 索引標籤，然後按兩下路徑。  
  
4.  在 [資料流程路徑編輯器] 中按一下 [一般]。 然後，您可以編輯路徑的預設名稱並提供路徑的描述。 您還可以修改 PathAnnotation 屬性。  
  
5.  按一下 **[確定]**。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="general-page---data-flow-path-editor"></a>[一般] 頁面-資料流程路徑編輯器
使用 **[資料流程路徑編輯器]** 對話方塊，即可設定路徑屬性、檢視資料行中繼資料，以及管理附加至路徑的資料檢視器。  
  
 使用 **[資料流程路徑編輯器]** 對話方塊的 **[一般]** 節點，即可命名和描述路徑，以及指定路徑註解的選項。  
  
### <a name="options"></a>選項。  
 **名稱**  
 提供路徑的唯一名稱。  
  
 **ID**  
 路徑的歷程識別碼。 此屬性是唯讀的。  
  
 **IdentificationString**  
 識別路徑的字串。 根據前面輸入的名稱自動產生。  
  
 **說明**  
 描述路徑。  
  
 **PathAnnotation**  
 指定要使用之註解的類型。 選擇 **[Never]** 以停用註解，選擇 **[AsNeeded]** 以視需要啟用註解，選擇 **[SourceName]** 以使用 **[SourceName]** 選項的值來自動註解，以及選擇 **[PathName]** 以使用 **[Name]** 屬性的值來自動註解。  
  
 **DestinationName**  
 顯示路徑末端的輸入。  
  
 **SourceName**  
 顯示路徑開頭的輸出。  
 
## <a name="metadata-page---data-flow-path-editor"></a>中繼資料] 頁面的 [資料流程路徑編輯器
使用 [資料流程路徑編輯器] 對話方塊的 [中繼資料] 頁面，即可檢視路徑資料行的中繼資料。  
  
### <a name="options"></a>選項。  
 **路徑中繼資料**  
 列出資料行中繼資料。 按一下資料行標題來排序資料行資料。  
  
 **名稱**  
 列出資料行名稱。  
  
 **資料類型**  
 列出資料行的資料類型。  
  
 **有效位數**  
 列出數值中的位數。  
  
 **小數位數**  
 列出數值中之小數點右邊的位數。  
  
 **長度**  
 列出資料行的目前長度。  
  
 **字碼頁**  
 列出資料行的字碼頁。 值為 **0** 時，指出資料行不使用字碼頁。 這是在資料為 Unicode 格式，或資料具有數值、日期或時間等資料類型時才會發生。  
  
 **排序索引鍵位置**  
 列出資料行的排序索引鍵位置。 值為 **0** 時，指出資料行並未排序。  
  
> [!NOTE]  
>  減號 (-) 前置詞指出資料行是以遞減的順序來排序。  
  
 **比較旗標**  
 列出套用至資料行的比較旗標。  
  
 **來源元件**  
 列出是資料行來源的資料流程元件。  
  
 **複製到剪貼簿**  
 將資料行中繼資料複製到剪貼簿。 依預設，所有中繼資料列都會加以複製，就像依目前顯示的順序加以排序一般。  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>資料檢視器頁面資料流程路徑編輯器
使用 **[資料流程路徑編輯器]** 對話方塊的 **[資料檢視器]** 頁面，即可管理附加至路徑的資料檢視器。  
  
### <a name="options"></a>選項。  
 **名稱**  
 列出資料檢視器。  
  
 **資料檢視器類型**  
 列出資料檢視器的類型。  
  
 **加入**  
 按一下即可使用 [設定資料檢視器] 對話方塊加入資料檢視器。  
  
 **Delete**  
 按一下即可刪除選取的資料檢視器。  
  
 **設定**  
 按一下即可使用 [設定資料檢視器] 對話方塊，來設定選取的資料檢視器。  
 
## <a name="path-properties"></a>路徑屬性
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中的資料流程物件具有元件層級、輸入和輸出層級，以及輸入資料行和輸出資料行層級上的通用屬性和自訂屬性。 許多屬性都有唯讀的值，這些值是在執行階段由資料流程引擎所指派。  
  
 本主題將列出及描述連接資料流程物件之路徑的自訂屬性。  
  
### <a name="custom-properties-of-a-path"></a>路徑的自訂屬性  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型中，連接資料流程中元件的路徑會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 介面。  
  
 下表將描述資料流程中路徑的可設定屬性。 資料流程引擎也會將值指派給這裡未列出的其他唯讀屬性。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|PathAnnotation|整數 (列舉)|指出設計師介面上是否應該與路徑一起顯示註解的值。 可能的值為 **AsNeeded**、 **SourceName**、 **PathName**和 **Never**。 預設值為 **AsNeeded**。|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|與路徑相關聯的輸入。|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|與路徑相關聯的輸出。|  

