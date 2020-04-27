---
title: 要求記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 521d40529501d761b8e50300c16a816284109695
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770884"
---
# <a name="request-log"></a>要求記錄檔
  使用 **[要求記錄檔]** 對話方塊可以檢視對 SAP Netweaver BW 系統提出資料取樣要求期間記錄的事件。 如果您需要疑難排解 SAP BW 來源的組態，這項資訊可能很有用。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源元件，請參閱 [SAP BW 來源](sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
 **若要開啟要求記錄檔對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤上，按兩下 SAP BW 來源。  
  
3.  在 **[SAP BW 來源編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在您設定 SAP BW 來源之後，請按一下 **[預覽]** ，即可在 **[要求記錄檔]** 對話方塊中預覽事件。  
  
    > [!NOTE]  
    >  按一下 **[預覽]** 也會開啟 **[預覽]** 對話方塊。 如需有關此對話方塊的詳細資訊，請參閱＜ [Preview](preview.md)＞。  
  
## <a name="options"></a>選項。  
 **Time**  
 顯示記錄事件的時間。  
  
 **型別**  
 顯示記錄的事件類型。 下表列出可能的事件類型。  
  
|值|描述|  
|-----------|-----------------|  
|S|成功訊息。|  
|E|錯誤訊息|  
|W|警告訊息。|  
|I|參考資訊。|  
|A|作業已中止。|  
  
 **訊息**  
 顯示與記錄之事件相關聯的訊息文字。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
