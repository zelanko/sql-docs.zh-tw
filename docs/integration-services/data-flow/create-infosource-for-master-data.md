---
title: 建立主要資料的 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d481544611f1246922fc16b1c89f16dcf745802
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750342"
---
# <a name="create-infosource-for-master-data"></a>[建立主要資料的 InfoSource]
  使用 [建立主要資料的 InfoSource] 對話方塊可以在 SAP Netweaver BW 系統中建立主要資料的新 InfoSource。  
  
 您可以從 [SAP BW 目的地編輯器] 的 [連線管理員] 頁面開啟 [建立主要資料的 InfoSource] 對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟建立主要資料的 InfoSource 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 [連線管理員] 頁面的 [建立 SAP BW 物件] 群組方塊中，選取 [InfoSource]，然後按一下 [建立]。  
  
5.  在 [建立 InfoSource] 對話方塊中，選取 [主要資料]，然後按一下 [確定]。  
  
## <a name="options"></a>選項。  
 **InfoObject 名稱**  
 輸入新 InfoSource 應該依據的 InfoObject 名稱。  
  
 **查閱**  
 查閱 InfoObject。 這個選項會開啟 [查閱 InfoObject] 對話方塊，讓您能夠選取 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md)＞。  
  
 在您選取 InfoObject 之後，此元件就會將選取之 InfoObject 的名稱填入 [InfoObject 名稱] 文字方塊。  
  
 **新增**  
 建立新的 InfoObject。 這個選項會開啟 [建立新的 InfoObject] 對話方塊，讓您能夠建立新的 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md)＞。  
  
 在您建立 InfoObject 之後，此元件就會將新 InfoObject 的名稱填入 [InfoObject 名稱] 文字方塊。  
  
 **簡短描述**  
 輸入新 InfoSource 的簡短描述。  
  
 **詳細描述**  
 輸入新 InfoSource 的詳細描述。  
  
 **來源系統**  
 選取要與新 InfoSource 相關聯的來源系統。  
  
 **應用程式**  
 輸入要與新 InfoSource 相關聯的應用程式名稱。  
  
 **屬性**  
 表示主要資料包含屬性。  
  
 **文字**  
 表示主要資料包含屬性。  
  
 **儲存並啟用**  
 儲存並啟用新的 InfoSource。  
  
## <a name="see-also"></a>另請參閱  
 [建立 InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
