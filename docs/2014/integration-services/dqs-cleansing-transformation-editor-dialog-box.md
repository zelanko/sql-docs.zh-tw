---
title: DQS 清理轉換編輯器對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eaff1c5ac8ae5a804f546fc5e551dcb62e2fda7a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966904"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>DQS 清理轉換編輯器對話方塊
  使用 [DQS 清理轉換編輯器]**** 對話方塊，即可更正使用 Data Quality Services (DQS) 的資料。 如需詳細資訊，請參閱 [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-services-concepts.md)。  
  
 若要了解有關轉換的詳細資訊，請參閱＜ [DQS Cleansing Transformation](data-flow/transformations/dqs-cleansing-transformation.md)＞。  
  
 **您想要做什麼事？**  
  
-   [開啟 DQS 清理轉換編輯器](#open)  
  
-   [設定 [連接管理員] 索引標籤上的選項](#connection)  
  
-   [設定對應索引標籤上的選項](#mapping)  
  
-   [設定進階索引標籤上的選項](#advanced)  
  
-   [設定 [DQS 清理連接管理員] 對話方塊中的選項](#manager)  
  
##  <a name="open-the-dqs-cleansing-transformation-editor"></a><a name="open"></a>開啟 DQS 清理轉換編輯器  
  
1.  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，將 DQS 清理轉換加入至 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]封裝。  
  
2.  以滑鼠右鍵按一下此元件，然後按一下 **[編輯]**。  
  
##  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> 設定連接管理員索引標籤上的選項  
 **資料品質連接管理員**  
 從清單中選取現有的 DQS 連線管理員，或按一下 [新增]**** 建立新的連線。  
  
 **新增**  
 使用 [DQS 清理連線管理員]**** 對話方塊來建立新的連線管理員。 請參閱[設定 DQS 清理連線管理員對話方塊中的選項](#manager)  
  
 **資料品質知識庫**  
 針對連接的資料來源選取現有的 DQS 知識庫。 如需有關 DQS 知識庫的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)＞。  
  
 **加密連接**  
 指定是否要加密連接，以便加密 DQS 伺服器與之間的資料傳輸 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
 **可用的定義域**  
 針對選取的知識庫列出可用的定義域。 定義域有二種類型：單一定義域以及包含兩個或多個單一定義域的複合定義域。  
  
 如需有關如何將資料行對應至複合定義域的詳細資訊，請參閱＜ [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)＞。  
  
 如需有關定義域的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)＞。  
  
 **設定錯誤輸出**  
 指定如何處理資料列層級錯誤。 當轉換更正來自所連接之資料來源資料所含的非預期資料值或驗證條件約束時，可能會發生錯誤。  
  
 有效的值如下：  
  
-   **[失敗元件]**，指出轉換失敗，且輸入資料未插入 Data Quality Services 資料庫中。 這是預設值。  
  
-   **[重新導向資料列]**，指出輸入資料未插入 Data Quality Services 資料庫，並會重新導向至錯誤輸出。  
  
##  <a name="set-options-on-the-mapping-tab"></a><a name="mapping"></a>在 [對應] 索引標籤上設定選項  
 如需有關如何將資料行對應至複合定義域的詳細資訊，請參閱＜ [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)＞。  
  
 **可用的輸入資料行**  
 從連接的資料來源列出資料行。 選取一個或多個包含您想要更正之資料的資料行。  
  
 **輸入資料行**  
 列出您在 [可用的輸入資料行]**** 區域中選取的輸入資料行。  
  
 **網域**  
 選取要對應至輸入資料行的定義域。  
  
 **來源別名**  
 列出包含原始資料行值的來源資料行。  
  
 按一下欄位以修改資料行名稱。  
  
 **輸出別名**  
 列出 [DQS 清理轉換]**** 所輸出的資料行。 此資料行包含原始資料行值或更正的值。  
  
 按一下欄位以修改資料行名稱。  
  
 **狀態別名**  
 列出包含更正資料之狀態資訊的資料行。 按一下欄位以修改資料行名稱。  
  
##  <a name="set-options-on-the-advanced-tab"></a><a name="advanced"></a>設定 [Advanced] 索引標籤上的選項  
 **標準化輸出**  
 指出是否要根據針對定義域所定義的輸出格式，以標準化格式輸出資料。 如需標準化格式的詳細資訊，請參閱 [資料清理](../../2014/data-quality-services/data-cleansing.md)。  
  
 **信心百倍**  
 指出是否要針對更正的資料包含信心層級。 信心層級表示 DQS 對更正或建議的確定程度。 如需信賴等級的詳細資訊，請參閱 [資料清理](../../2014/data-quality-services/data-cleansing.md)。  
  
 **原因**  
 指出是否要包含資料更正的原因。  
  
 **附加的資料**  
 指出是否要輸出從現有參考資料提供者收到的其他資料。 如需詳細資訊，請參閱 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)。  
  
 **附加的資料結構描述**  
 指出是否要輸出資料結構描述。 如需詳細資訊，請參閱[將定義域或複合定義域附加至參考資料](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)。  
  
##  <a name="set-the-options-in-the-dqs-cleansing-connection-manager-dialog-box"></a><a name="manager"></a>設定 [DQS 清理連接管理員] 對話方塊中的選項  
 **伺服器名稱**  
 選取或輸入您想要連接之 DQS 伺服器的名稱。 如需有關伺服器的詳細資訊，請參閱＜ [DQS Administration](../../2014/data-quality-services/dqs-administration.md)＞。  
  
 **測試連接**  
 按一下以確認您指定的連接是否可用。  
  
 您也可以透過執行下列步驟，從連接區域開啟 **[DQS 清理連接管理員]** 對話方塊：  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟現有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，或建立新的專案。  
  
2.  以滑鼠右鍵按一下連接區域、按一下 [新增連接]****，然後按一下 [DQS]****。  
  
3.  按一下 [新增] 。  
  
## <a name="see-also"></a>另請參閱  
 [將資料品質規則套用至資料來源](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  
