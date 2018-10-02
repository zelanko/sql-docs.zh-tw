---
title: 查閱 InfoObject | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6246042a70aca4edc07a36bc0dabe95be56c6d7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657969"
---
# <a name="look-up-infoobject"></a>查閱 InfoObject
  使用 [查閱 InfoObject] 對話方塊可以查閱 SAP Netweaver BW 系統中定義的 InfoObject。 出現可用的 InfoObject 清單時，請選取您要的 InfoObject，然後 SAP BW 目的地就會將必要的值填入相關聯的選項。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地會使用 [查閱 InfoObject] 對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟查閱 InfoObject 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 [連線管理員] 頁面的 [建立 SAP BW 物件] 群組方塊中，選取下列其中一個選項：  
  
    1.  選取 [InfoCube]。 然後，按一下 [建立]。 在 [建立交易資料的 InfoCube] 對話方塊中，於清單內其中一個資料列的 [IObject] 資料行中，按一下 [搜尋]。 每個資料列都代表封裝之資料流程中的資料行。  
  
    2.  選取 [InfoSource]。 然後，按一下 [建立]。 在 [建立 InfoSource] 對話方塊中，選取 [交易資料]。 在 [建立交易資料的 InfoSource] 對話方塊中，於清單內其中一個資料列的 [IObject] 資料行中，按一下 [搜尋]。 每個資料列都代表封裝之資料流程中的資料行。  
  
    3.  選取 [InfoSource]。 然後，按一下 [建立]。 在 [建立 InfoSource] 對話方塊中，選取 [主要資料]。 在 [建立主要資料的 InfoSource] 對話方塊中，按一下 [查閱]。  
  
 您也可以在 [建立新的 InfoObject] 對話方塊的 [屬性] 區段中按一下 [加入]，藉以開啟 [查閱 InfoObject] 對話方塊。  
  
## <a name="lookup-options"></a>查閱選項  
 在查閱欄位文字方塊中，您可以使用星號萬用字元 (*) 或結合星號萬用字元使用部分字串來篩選結果。 不過，如果您將查閱欄位保留空白，查閱處理序就只會比對該欄位中的空白字串。  
  
 **特性**  
 查閱代表特性的 InfoObject。  
  
 **單位**  
 查閱代表單位的 InfoObject。  
  
 **關鍵數據**  
 查閱代表關鍵數據的 InfoObject。  
  
 **時間特性**  
 查閱代表時間特性的 InfoObject。  
  
 **名稱**  
 輸入您想要查閱的 InfoObject 名稱，或是包含星號萬用字元 (*) 的部分名稱。 或者，單獨使用星號萬用字元來包含所有 InfoObject。  
  
 **說明**  
 輸入描述，或是包含星號萬用字元 (*) 的部分描述。 或者，單獨使用星號萬用字元來包含所有 InfoObject (不論描述為何)。  
  
 **查閱**  
 查閱 SAP Netweaver BW 系統中定義的相符 InfoObject。  
  
## <a name="lookup-results"></a>查閱結果  
 在您按一下 [查閱] 按鈕之後，SAP Netweaver BW 系統中的 InfoObject 清單就會顯示在包含下列資料行標題的資料表中。  
  
 **InfoObject**  
 顯示 SAP Netweaver BW 系統中定義的 InfoObject 名稱。  
  
 **文字 (短)**  
 顯示與 InfoObject 相關聯的簡短文字。  
  
 出現可用的 InfoObject 清單時，請選取您要的 InfoObject，然後目的地就會將必要的值填入相關聯的選項。  
  
## <a name="see-also"></a>另請參閱  
 [建立交易資料的 InfoCube](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [建立 InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [建立交易資料的 InfoSource](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [建立主要資料的 InfoSource](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [建立新的 InfoObject](../../integration-services/data-flow/create-new-infoobject.md)   
 [SAP BW 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
