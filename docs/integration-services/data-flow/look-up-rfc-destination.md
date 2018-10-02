---
title: 查閱 RFC 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 448211ee1acbfb318e8ed8f1be5161fb5a18a94e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617946"
---
# <a name="look-up-rfc-destination"></a>查閱 RFC 目的地
  使用 [查閱 RFC 目的地] 對話方塊可以查閱 SAP Netweaver BW 系統中定義的 RFC 目的地。 出現可用的 RFC 目的地清單時，請選取您要的目的地，然後此元件就會將必要的值填入相關聯的選項。  
  
 SAP BW 來源和 SAP BW 目的地都會使用 [查閱 RFC 目的地] 對話方塊。 如需 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 這些元件的詳細資訊，請參閱 [SAP BW 來源](../../integration-services/data-flow/sap-bw-source.md)和 [SAP BW 目的地](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟查閱 RFC 目的地對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源或目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 SAP BW 來源或目的地。  
  
3.  在 [SAP BW 來源編輯器] 或 [SAP BW 目的地編輯器] 中，按一下 [連線管理員] 開啟編輯器的 [連線管理員] 頁面。  
  
4.  在 [連線管理員] 頁面的 [RFC 目的地] 群組方塊中，按一下 [查閱] 顯示 [查閱 RFC 目的地] 對話方塊。  
  
     在 [SAP BW 來源編輯器] 中，只有當 [執行模式] 的值是 [P - 觸發處理鏈結] 或 [W - 等候通知] 時，才會出現 [RFC 目的地] 群組方塊。  
  
## <a name="options"></a>選項。  
 **目的地**  
 檢視 SAP Netweaver BW 系統中定義的 RFC 目的地名稱。  
  
 **閘道器主機**  
 檢視閘道器主機的伺服器名稱或 IP 位址。 此名稱或 IP 位址通常與 SAP 應用程式伺服器相同。  
  
 **閘道器服務**  
 以 **sapgwNN**格式檢視閘道器服務的名稱，其中 **NN** 是系統編號。  
  
 **程式識別碼**  
 檢視與 RFC 目的地相關聯的程式識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
