---
title: 設定資料流程元件的屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ac3714dbbd96150aa9d670e370e8a475f6a57e1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817950"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>設定資料流程元件的屬性
  若要設定資料流程元件的屬性 (包括來源、目的地和轉換)，請使用下列其中一個功能：  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的元件編輯器。 這些編輯器僅包括每個資料流程元件的自訂屬性。  
  
-   [屬性] 視窗會列出每個元素的元件層級自訂屬性，以及所有資料流程元素通用的屬性。  
  
-   [進階編輯器] 對話方塊可讓您存取每一個元件的自訂屬性。 [進階編輯器] 對話方塊也可讓您存取所有資料流程元件的屬性，也就是輸入、輸出、錯誤輸出、資料行和外部資料行的屬性。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>使用元件編輯器設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含資料流程 (具有您要檢視及修改其屬性之元件) 的「資料流程」工作。  
  
4.  按兩下資料流程元件。  
  
5.  在元件編輯器中，檢視或修改屬性值，然後關閉編輯器。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>使用屬性視窗設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含您要檢視及修改其屬性之元件的「資料流程」工作。  
  
4.  以滑鼠右鍵按一下資料流程元件，然後按一下 [屬性]。  
  
5.  檢視或修改屬性值，然後關閉 [屬性] 視窗。  
  
    > [!NOTE]  
    >  許多屬性都是唯讀的，因此無法修改。  
  
6.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>使用進階編輯器設定資料流程元件的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含您要檢視或修改之元件的「資料流程」工作。  
  
4.  在資料流程設計師中，以滑鼠右鍵按一下資料流程元件，然後按一下 [顯示進階編輯器]。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，支援多個輸入的資料流程元件無法使用 [進階編輯器]。  
  
5.  在 [進階編輯器] 對話方塊中，執行下列任何一個步驟：  
  
    -   若要檢視及指定此元件所使用的連接，請按一下 [連線管理員] 索引標籤。  
  
        > [!NOTE]  
        >  [連線管理員] 索引標籤只可用於使用連線管理員連接到資料來源 (例如檔案和資料庫) 的資料流程元件  
  
    -   若要檢視和修改元件層級屬性，請按一下 [元件屬性] 索引標籤。  
  
    -   若要檢視和修改外部資料行與可用輸出之間的對應，請按一下 [資料行對應] 索引標籤。  
  
        > [!NOTE]  
        >  [資料行對應] 索引標籤只能在檢視或編輯來源或目的地時使用。  
  
    -   若要檢視可用輸入資料行的清單並更新輸出資料行的名稱，請按一下 [輸入資料行] 索引標籤。  
  
        > [!NOTE]  
        >  [輸入資料行] 索引標籤僅在使用轉換或目的地時可用。 如需詳細資訊，請參閱 [Integration Services 轉換](transformations/integration-services-transformations.md)。  
  
    -   若要檢視和修改輸入、輸出及錯誤輸出的屬性，以及檢視和修改其包含之資料行的屬性，請按一下 [輸入與輸出屬性] 索引標籤。  
  
        > [!NOTE]  
        >  來源沒有輸入。 除了選擇性的錯誤輸出之外，目的地沒有輸出。  
  
6.  檢視或修改屬性值。  
  
7.  按一下 [確定] 。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 轉換](transformations/integration-services-transformations.md)  
  
  
