---
title: SAP BW 目的地編輯器 (連線管理員頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.connection.f1
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ed9d2a03f0982f90aae9c57334a4fa543d176ab4
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289484"
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>SAP BW 目的地編輯器 (連接管理員頁面)
  使用 **[SAP BW 目的地編輯器]** 的 **[連接管理員]** 頁面可以選取 SAP BW 目的地將使用的 SAP BW 連接管理員。 在這個頁面上，您也可以選取將資料載入 SAP Netweaver BW 系統中所用的參數。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地，請參閱 [SAP BW 目的地](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **開啟連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定目的地的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **SAP BW 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [SAP BW 連線管理員] 對話方塊來建立新的連線管理員。  
  
 **測試負載**  
 執行載入程序的測試，這項測試會使用您已選取的設定，但是不會載入任何資料列。  
  
### <a name="infopackageinfosource-options"></a>InfoPackage/InfoSource 選項  
 您不需要事先了解並輸入這些值。 使用 **[查閱]** 按鈕，即可尋找並選取適當的 InfoPackage。 在您選取 InfoPackage 之後，此元件就會針對這些選項輸入適當的值。  
  
 **InfoPackage**  
 輸入 InfoPackage 的名稱。  
  
 **InfoSource**  
 輸入 InfoSource 的名稱。  
  
 **型別**  
 輸入可識別 InfoSource 類型的單一字元。 下表列出可接受的單一字元值。  
  
|Value|Description|  
|-----------|-----------------|  
|**D**|交易資料|  
|**M**|主要資料|  
|**T**|文字|  
|**H**|階層資料|  
  
 **邏輯系統**  
 輸入與 InfoPackage 相關聯之邏輯系統的名稱。  
  
 **查閱**  
 使用 [查閱 InfoPackage] 對話方塊來查閱 InfoPackage。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up InfoPackage](../../integration-services/data-flow/look-up-infopackage.md)＞。  
  
### <a name="rfc-destination-options"></a>RFC 目的地選項  
 您不需要事先了解並輸入這些值。 使用 **[查閱]** 按鈕，即可尋找並選取適當的 RFC 目的地。 在您選取 RFC 目的地之後，此元件就會針對這些選項輸入適當的值。  
  
 **閘道器主機**  
 輸入閘道器主機的伺服器名稱或 IP 位址。 此名稱或 IP 位址通常與 SAP 應用程式伺服器相同。  
  
 **閘道器服務**  
 以 **sapgwNN**格式輸入閘道器服務的名稱，其中 **NN** 是系統編號。  
  
 **程式識別碼**  
 輸入與 RFC 目的地相關聯的程式識別碼。  
  
 **查閱**  
 使用 [查閱 RFC 目的地] 對話方塊來查閱 RFC 目的地。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md)＞。  
  
### <a name="create-sap-bw-objects-options"></a>建立 SAP BW 物件選項  
 **選取 物件類型**  
 選取您想要建立的 SAP Netweaver BW 物件類型。 您可以選取下列其中一種類型：  
  
-   [InfoObject]  
  
-   InfoCube  
  
-   InfoSource  
  
-   InfoPackage  
  
 **建立**  
 建立選取的 SAP Netweaver BW 物件類型。  
  
|物件類型|結果|  
|-----------------|------------|  
|**InfoObject**|使用 **[建立新的 InfoObject]** 對話方塊來建立新的 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md)＞。|  
|**InfoCube**|使用 **[建立交易資料的 InfoCube]** 對話方塊來建立新的 InfoCube。 如需有關此對話方塊的詳細資訊，請參閱＜ [Create InfoCube for Transaction Data](../../integration-services/data-flow/create-infocube-for-transaction-data.md)＞。|  
|**InfoSource**|使用 **[建立 InfoSource]** 對話方塊，然後使用 **[建立交易資料的 InfoSource]** 或 **[建立主要資料的 InfoSource]** 對話方塊來建立新的 InfoSource。 如需有關這些對話方塊的詳細資訊，請參閱＜ [Create InfoSource](../../integration-services/data-flow/create-infosource.md)＞、＜ [Create InfoSource for Transaction Data](../../integration-services/data-flow/create-infosource-for-transaction-data.md) ＞和＜ [Create InfoSource for Master Data](../../integration-services/data-flow/create-infosource-for-master-data.md)＞。|  
|**InfoPackage**|使用 **[建立 InfoPackage]** 對話方塊來建立新的 InfoPackage。 如需有關此對話方塊的詳細資訊，請參閱＜ [Create InfoPackage](../../integration-services/data-flow/create-infopackage.md)＞。|  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 目的地編輯器 &#40;進階頁面&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
