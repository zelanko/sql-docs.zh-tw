---
title: 建立交易資料的 InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab5f23e2-cd4e-4507-83d9-ac5ef721c171
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c18c6edb21effe53c31e7885ec25025c94c4f1d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162730"
---
# <a name="create-infosource-for-transaction-data"></a>建立交易資料的 InfoSource
  使用 [建立交易資料的 InfoSource] 對話方塊可以在 SAP Netweaver BW 系統中建立交易資料的新 InfoSource。  
  
 您可以從 [SAP BW 目的地編輯器] 的 [連線管理員] 頁面開啟 [建立交易資料的 InfoSource] 對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟建立交易資料的 InfoSource 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 [連線管理員] 頁面的 [建立 SAP BW 物件] 群組方塊中，選取 [InfoSource]，然後按一下 [建立]。  
  
5.  在 [建立 InfoSource] 對話方塊中，選取 [交易資料]，然後按一下 [確定]。  
  
## <a name="general-options"></a>一般選項  
 **InfoSource 名稱**  
 輸入新 InfoSource 的名稱。  
  
 **簡短描述**  
 輸入新 InfoSource 的簡短描述。  
  
 **詳細描述**  
 輸入新 InfoSource 的詳細描述。  
  
 **來源系統**  
 選取與 InfoSource 相關聯的來源系統。  
  
 **儲存並啟用**  
 儲存並啟用新的 InfoSource。  
  
## <a name="infosource-transfer-structure-options"></a>InfoSource 傳送結構選項  
 InfoSource 傳送結構可讓您將資料流程資料行與 InfoSource 建立關聯。  
  
 **PipelineElement**  
 在連接到 SAP BW 目的地之資料流程的輸出中顯示資料行。  
  
 **PipelineDataType**  
 顯示資料流程資料行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。  
  
 **Iobject - 搜尋**  
 將現有的 InfoObject 與目前資料列中的資料流程資料行建立關聯。 若要建立此關聯，請按一下 [搜尋]，然後使用 [查閱 InfoObject] 對話方塊來選取現有的 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up InfoObject](look-up-infoobject.md)＞。  
  
 在您選取現有的 InfoObject 之後，此元件就會將選取的值填入 [InfoObject] 和 [類型] 資料行。  
  
 **Iobject - 新增**  
 建立新的 InfoObject 並將這個新的 InfoObject 與目前資料列中的資料流程資料行建立關聯。 若要建立新的 InfoObject，請按一下 [新增]，然後使用 [建立新的 InfoObject] 對話方塊來建立 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Create New InfoObject](create-new-infoobject.md)＞。  
  
 在您建立新的 InfoObject 之後，此元件就會將新的值填入 [InfoObject] 和 [類型] 資料行。  
  
 **Iobject - 移除**  
 移除 InfoObject 與目前資料列的資料流程資料行之間的關聯。 若要移除此關聯，請按一下 [移除]。  
  
 **InfoObject**  
 顯示與資料流程資料行相關聯的 InfoObject 名稱。  
  
 **型別**  
 顯示與資料流程資料行相關聯的 InfoObject 類型。 下表列出類型的可能值。  
  
|值|描述|  
|-----------|-----------------|  
|CHA|特性|  
|UNI|單位|  
|KYF|關鍵數據|  
|TIM|時間特性|  
  
 **單位欄位**  
 指定 InfoObject 將使用的單位。  
  
## <a name="see-also"></a>另請參閱  
 [建立 InfoSource](create-infosource.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
