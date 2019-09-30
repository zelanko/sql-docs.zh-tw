---
title: 要求記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4a84025efefa397cd1f33a706073faceb0ad70ae
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292123"
---
# <a name="request-log"></a>要求記錄檔

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 **[要求記錄檔]** 對話方塊可以檢視對 SAP Netweaver BW 系統提出資料取樣要求期間記錄的事件。 如果您需要疑難排解 SAP BW 來源的組態，這項資訊可能很有用。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源元件，請參閱 [SAP BW 來源](../../integration-services/data-flow/sap-bw-source.md)。  
  
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
    >  按一下 **[預覽]** 也會開啟 **[預覽]** 對話方塊。 如需有關此對話方塊的詳細資訊，請參閱＜ [Preview](../../integration-services/data-flow/preview.md)＞。  
  
## <a name="options"></a>選項。  
 **Time**  
 顯示記錄事件的時間。  
  
 **型別**  
 顯示記錄的事件類型。 下表列出可能的事件類型。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|S|成功訊息。|  
|E|錯誤訊息|  
|W|警告訊息。|  
|I|參考資訊。|  
|只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時，|作業已中止。|  
  
 **訊息**  
 顯示與記錄之事件相關聯的訊息文字。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
