---
title: "查閱處理序鏈結 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caffa747cb67469c96675e10d7c3904ac8e77aa0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="look-up-process-chain"></a>查閱 ProcessChain
  使用 **[查閱 ProcessChain]** 對話方塊可以查閱 SAP Netweaver BW 系統中定義的處理序鏈結。 出現可用的處理序鏈結清單時，請選取您要的鏈結，然後來源就會將必要的值填入相關聯的選項。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源會使用 **[查閱 ProcessChain]** 對話方塊。 若要了解有關 SAP BW 來源的詳細資訊，請參閱＜ [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md)＞。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟查閱 ProcessChain 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 來源。  
  
3.  在 **[SAP BW 來源編輯器]**中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 **[處理序鏈結]** 群組方塊中，按一下 **[查閱]** 顯示 **[查閱 ProcessChain]** 對話方塊。  
  
     只有當 [執行模式] 的值是 [P - 觸發處理鏈結] 時，才會出現 [處理序鏈結] 群組方塊。  
  
## <a name="lookup-options"></a>查閱選項  
 在查閱欄位中，您可以使用星號萬用字元 (*) 或結合星號萬用字元使用部分字串來篩選結果。 不過，如果您將查閱欄位保留空白，查閱作業就只會比對該欄位中的空白字串。  
  
 **Process chain**  
 輸入您想要查閱的處理序鏈結名稱，或輸入包含星號萬用字元 (*) 的部分名稱。 或者，單獨使用星號萬用字元來包含所有處理序鏈結。  
  
 **[查閱]**  
 查閱 SAP Netweaver BW 系統中定義的相符處理序鏈結。  
  
## <a name="lookup-results"></a>查閱結果  
 在您按一下 [查閱] 按鈕之後，SAP Netweaver BW 系統中的處理序鏈結清單就會顯示在包含下列資料行標題的資料表中：  
  
 **[處理序鏈結]**  
 顯示 SAP Netweaver BW 系統中定義的處理序鏈結名稱。  
  
 **說明**  
 顯示處理序鏈結的描述。  
  
 出現可用的處理序鏈結清單時，請選取您要的鏈結，然後來源就會將必要的值填入相關聯的選項。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
