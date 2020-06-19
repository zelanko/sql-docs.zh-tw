---
title: 查閱 InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7c0cb7a4-cd07-44cc-85cb-eb1ad91f85fd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c179f285ab12918aed7cd64a8df3341c6c333a94
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915409"
---
# <a name="look-up-infopackage"></a>查閱 InfoPackage
  使用 [查閱 InfoPackage]  對話方塊可以查閱 SAP Netweaver BW 系統中定義的 InfoPackage。 出現 InfoPackage 的清單時，請選取您要的 InfoPackage，然後目的地就會將必要的值填入相關聯的選項。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地會使用 [查閱 ProcessChain]  對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟查閱 InfoPackage 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程]  索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 [連線管理員]  頁面的 [InfoPackage/InfoSource]  群組方塊中，按一下 [查閱]  顯示 [查閱 InfoPackage]  對話方塊。  
  
## <a name="lookup-options"></a>查閱選項  
 在查閱欄位中，您可以使用星號萬用字元 (*) 或結合星號萬用字元使用部分字串來篩選結果。 不過，如果您將查閱欄位保留空白，查閱作業就只會比對該欄位中的空白字串。  
  
 **InfoPackage**  
 輸入您想要查閱的 InfoPackage 名稱，或是包含星號萬用字元 (*) 的部分名稱。 或者，單獨使用星號萬用字元來包含所有 InfoPackage。  
  
 **InfoSource**  
 輸入 InfoSource 的名稱，或是包含星號萬用字元 (*) 的部分名稱。 或者，單獨使用星號萬用字元來包含所有 InfoPackage (不論 InfoSource 為何)。  
  
 **來源系統**  
 輸入來源系統的名稱，或是包含星號萬用字元 (*) 的部分名稱。 或者，單獨使用星號萬用字元來包含所有 InfoPackage (不論來源系統為何)。  
  
 **查閱**  
 查閱 SAP Netweaver BW 系統中定義的相符 InfoPackage。  
  
## <a name="lookup-results"></a>查閱結果  
 在您按一下 [查閱] 按鈕之後，SAP Netweaver BW 系統中的 InfoPackage 清單就會顯示在包含下列資料行標題的資料表中。  
  
 **InfoPackage**  
 顯示 SAP Netweaver BW 系統中定義的 InfoPackage 名稱。  
  
 **型別**  
 顯示 InfoPackage 的類型。 下表列出類型的可能值。  
  
|值|描述|  
|-----------|-----------------|  
|Trans.|交易資料。|  
|Attr.|屬性資料。|  
|文字|文字。|  
  
 **說明**  
 顯示 InfoPackage 的描述。  
  
 **InfoSource**  
 顯示與 InfoPackage 相關聯的 InfoSource 名稱 (如果有的話)。  
  
 **Source System**  
 顯示來源系統的名稱。  
  
 出現 InfoPackage 的清單時，請選取您要的 InfoPackage，然後目的地就會將必要的值填入相關聯的選項。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 目的地編輯器 &#40;連線管理員頁面&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
