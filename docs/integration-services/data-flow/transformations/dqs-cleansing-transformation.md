---
title: "DQS 清理轉換 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssdqs.designer.cleansing.f1
- sql13.SSDQS.DESIGNER.DQCONNECTION.F1
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8cf75ff26033b7f6d2dd29af0d226b6b0172c094
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="dqs-cleansing-transformation"></a>DQS 清理轉換
  DQS 清理轉換會使用 Data Quality Services (DQS) 來更正連接之資料來源的資料，方法是套用針對所連接資料來源或相似資料來源而建立的核准規則。 如需有關資料更正規則的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)＞。 如需有關 DQS 的詳細資訊，請參閱＜ [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)＞。  
  
 為了判斷資料是否必須更正，DQS 清理轉換會在符合下列條件的情況下，處理來自輸入資料行的資料：  
  
-   已選擇要進行資料更正的資料行。  
  
-   可支援對該資料行的資料類型進行資料更正。  
  
-   資料行對應至具有相容資料類型的定義域。  
  
 轉換還包括您設定來處理資料列層級錯誤的錯誤輸出。 若要設定錯誤輸出，請使用 **[DQS 清理轉換編輯器]**。  
  
 您可以在資料流程中包括 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) ，用於識別資料中可能重複的資料列。  
  
## <a name="data-quality-projects-and-values"></a>資料品質專案及值  
 當您使用 DQS 清理轉換處理資料時，會在資料品質伺服器上建立清理專案。 您可以使用 Data Quality Client 管理專案。 此外，您也可以使用 Data Quality Client 將專案值匯入 DQS 知識庫定義域。 您可以只將值匯入設定為使用 DQS 清理轉換的定義域 (或連結的定義域)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [在 Data Quality Client 中開啟 Integration Services 專案](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Import Cleansing Project Values into a Domain](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [將資料品質規則套用至資料來源](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>相關內容  
  
-   [開啟、解除鎖定、重新命名和刪除資料品質專案](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   social.technet.microsoft.com 上的文章： [使用複合定義域清理複雜的資料](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)。  
  
## <a name="dqs-cleansing-transformation-editor-dialog-box"></a>DQS 清理轉換編輯器對話方塊
  使用 [DQS 清理轉換編輯器] 對話方塊，即可更正使用 Data Quality Services (DQS) 的資料。 如需詳細資訊，請參閱 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)。  
  
 **您想要做什麼事？**  
  
-   [開啟 DQS 清理轉換編輯器](#open)  
  
-   [設定連接管理員索引標籤上的選項](#connection)  
  
-   [設定對應索引標籤上的選項](#mapping)  
  
-   [設定進階索引標籤上的選項](#advanced)  
  
-   [設定 DQS 清理連接管理員對話方塊中的選項](#manager)  
  
###  <a name="open"></a> 開啟 DQS 清理轉換編輯器  
  
1.  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中，將 DQS 清理轉換加入至 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]封裝。  
  
2.  以滑鼠右鍵按一下此元件，然後按一下 **[編輯]**。  
  
###  <a name="connection"></a> 設定連接管理員索引標籤上的選項  
 **資料品質連接管理員**  
 從清單中選取現有的 DQS 連線管理員，或按一下 [新增] 建立新的連線。  
  
 **新增**  
 使用 [DQS 清理連線管理員] 對話方塊來建立新的連線管理員。 請參閱 [設定 DQS 清理連線管理員對話方塊中的選項](#manager)  
  
 **資料品質知識庫**  
 針對連接的資料來源選取現有的 DQS 知識庫。 如需有關 DQS 知識庫的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)＞。  
  
 **加密連接**  
 指定是否要加密連接，以便加密 DQS 伺服器與 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]之間的資料傳輸。  
  
 **可用的定義域**  
 針對選取的知識庫列出可用的定義域。 定義域有二種類型：單一定義域以及包含兩個或多個單一定義域的複合定義域。  
  
 如需有關如何將資料行對應至複合定義域的詳細資訊，請參閱＜ [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md)＞。  
  
 如需有關定義域的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)＞。  
  
 **設定錯誤輸出**  
 指定如何處理資料列層級錯誤。 當轉換更正來自所連接之資料來源資料所含的非預期資料值或驗證條件約束時，可能會發生錯誤。  
  
 有效的值如下：  
  
-   **[失敗元件]**，指出轉換失敗，且輸入資料未插入 Data Quality Services 資料庫中。 這是預設值。  
  
-   **[重新導向資料列]**，指出輸入資料未插入 Data Quality Services 資料庫，並會重新導向至錯誤輸出。  
  
###  <a name="mapping"></a> 設定對應索引標籤上的選項  
 如需有關如何將資料行對應至複合定義域的詳細資訊，請參閱＜ [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md)＞。  
  
 **可用的輸入資料行**  
 從連接的資料來源列出資料行。 選取一個或多個包含您想要更正之資料的資料行。  
  
 **輸入資料行**  
 列出您在 [可用的輸入資料行] 區域中選取的輸入資料行。  
  
 **網域**  
 選取要對應至輸入資料行的定義域。  
  
 **來源別名**  
 列出包含原始資料行值的來源資料行。  
  
 按一下欄位以修改資料行名稱。  
  
 **輸出別名**  
 列出 [DQS 清理轉換] 所輸出的資料行。 此資料行包含原始資料行值或更正的值。  
  
 按一下欄位以修改資料行名稱。  
  
 **狀態別名**  
 列出包含更正資料之狀態資訊的資料行。 按一下欄位以修改資料行名稱。  
  
###  <a name="advanced"></a> 設定進階索引標籤上的選項  
 **標準化輸出**  
 指出是否要根據針對定義域所定義的輸出格式，以標準化格式輸出資料。 如需標準化格式的詳細資訊，請參閱 [資料清理](../../../data-quality-services/data-cleansing.md)。  
  
 **信心**  
 指出是否要針對更正的資料包含信心層級。 信心層級表示 DQS 對更正或建議的確定程度。 如需信賴等級的詳細資訊，請參閱 [資料清理](../../../data-quality-services/data-cleansing.md)。  
  
 **Reason**  
 指出是否要包含資料更正的原因。  
  
 **附加的資料**  
 指出是否要輸出從現有參考資料提供者收到的其他資料。 如需詳細資訊，請參閱 [Reference Data Services in DQS](../../../data-quality-services/reference-data-services-in-dqs.md)。  
  
 **附加的資料結構描述**  
 指出是否要輸出資料結構描述。 如需詳細資訊，請參閱 [將定義域或複合定義域附加至參考資料](../../../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)。  
  
###  <a name="manager"></a> 設定 DQS 清理連接管理員對話方塊中的選項  
 **伺服器名稱**  
 選取或輸入您想要連接之 DQS 伺服器的名稱。 如需有關伺服器的詳細資訊，請參閱＜ [DQS Administration](../../../data-quality-services/dqs-administration.md)＞。  
  
 **測試連接**  
 按一下以確認您指定的連接是否可用。  
  
 您也可以透過執行下列步驟，從連接區域開啟 **[DQS 清理連接管理員]** 對話方塊：  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟現有的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案，或建立新的專案。  
  
2.  以滑鼠右鍵按一下連接區域、按一下 [新增連接]，然後按一下 [DQS]。  
  
3.  按一下 **[加入]**。  
  
