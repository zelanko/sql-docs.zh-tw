---
title: 建立 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 270f2831b814144f6e053db32509e27ffef02ba2
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727053"
---
# <a name="create-infosource"></a>建立 InfoSource

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  使用 [建立 InfoSource] 對話方塊可以建立新的 InfoSource。 若要建立新的 InfoSource，您可以使用 [建立交易資料的 InfoSource] 或 [建立主要資料的 InfoSource] 對話方塊。  
  
 您可以從 [SAP BW 目的地編輯器] 的 [連線管理員] 頁面開啟 [建立 InfoSource] 對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟建立 InfoSource 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 [連線管理員] 頁面的 [建立 SAP BW 物件] 群組方塊中，選取 [InfoSource]，然後按一下 [建立]。  
  
## <a name="options"></a>選項。  
 **交易資料**  
 建立交易資料的新 InfoSource。  
  
 如果您選取此選項，就會開啟 [建立交易資料的 InfoSource] 對話方塊。 您可以使用 [建立交易資料的 InfoSource] 對話方塊來建立新的 InfoSource。 如需此對話方塊的詳細資訊，請參閱 [建立交易資料的 InfoSource](../../integration-services/data-flow/create-infosource-for-transaction-data.md)。  
  
 **主要資料**  
 建立主要資料的新 InfoSource。  
  
 如果您選取此選項，就會開啟 [建立主要資料的 InfoSource] 對話方塊。 您可以使用 [建立主要資料的 InfoSource] 對話方塊來建立新的 InfoSource。 如需此對話方塊的詳細資訊，請參閱[建立主要資料的 InfoSource](../../integration-services/data-flow/create-infosource-for-master-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
