---
title: 建立新的 InfoObject | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3587a633-1c0b-4d63-a22a-6b2b93923c3a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e5d0ac61e65618527d5da8c7a8bcf2b5808b143
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290764"
---
# <a name="create-new-infoobject"></a>建立新的 InfoObject
  使用 **[建立新的 InfoObject]** 對話方塊可以在 SAP Netweaver BW 系統中建立新的 InfoObject。  
  
 您可以從 **[SAP BW 目的地編輯器]** 的 **[連接管理員]** 頁面開啟 **[建立 InfoObject]** 對話方塊。 若要深入了解 SAP BW 目的地，請參閱 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟建立新的 InfoObject 對話方塊**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 **[SAP BW 目的地編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
4.  在 **[連接管理員]** 頁面的 **[建立 SAP BW 物件]** 群組方塊中，執行下列其中一個步驟以建立 InfoObject：  
  
    1.  若要直接建立 InfoObject，請選取 **[InfoObject]**，然後按一下 **[建立]** 開啟 **[建立新的 InfoObject]** 對話方塊。  
  
    2.  若要在建立 InfoCube 時建立 InfoObject，請選取 **[InfoCube]**，然後按一下 **[建立]**。 在 **[建立交易資料的 InfoCube]** 對話方塊中，於清單內其中一個資料列的 **[IObject]** 資料行中，選取 **[建立]** 開啟 **[建立新的 InfoObject]** 對話方塊。  
  
        > [!NOTE]  
        >  資料表中的每個資料列都代表封裝之資料流程中的資料行。  
  
    3.  若要在建立交易資料的 InfoSource 時建立 InfoObject，請選取 **[InfoSource]**，然後按一下 **[建立]**。 在 **[建立 InfoSource]** 對話方塊中，選取 **[交易資料]**，然後按一下 **[確定]**。 在 **[建立交易資料的 InfoSource]** 對話方塊中，於清單內其中一個資料列的 **[IObject]** 資料行中，選取 **[建立]** 開啟 **[建立新的 InfoObject]** 對話方塊。  
  
        > [!NOTE]  
        >  資料表中的每個資料列都代表封裝之資料流程中的資料行。  
  
    4.  若要在建立主要資料的 InfoSource 時建立 InfoObject，請選取 **[InfoSource]**，然後按一下 **[建立]**。 在 **[建立 InfoSource]** 對話方塊中，選取 **[主要資料]**，然後按一下 **[確定]**。 在 **[建立主要資料的 InfoSource]** 對話方塊中，按一下 **[新增]** 開啟 **[建立新的 InfoObject]** 對話方塊。  
  
 您也可以在 **[建立新的 InfoObject]** 對話方塊的 **[屬性]** 區段中按一下 **[新增]** ，藉以開啟 **[建立新的 InfoObject]** 對話方塊。  
  
## <a name="general-options"></a>一般選項  
 **特性**  
 建立代表維度資料的 InfoObject。  
  
 **關鍵數據**  
 建立代表事實資料的 InfoObject。  
  
 **InfoObject 名稱**  
 輸入 InfoObject 的名稱。  
  
 **簡短描述**  
 輸入 InfoObject 的簡短描述。  
  
 **詳細描述**  
 輸入 InfoObject 的詳細描述。  
  
 **具有主要資料**  
 表示 InfoObject 包含屬性、文字或階層形式的主要資料。  
  
> [!NOTE]  
>  如果 InfoObject 代表維度資料，而且您已選取 [特性] 選項，請選取此選項。  
  
 **允許小寫字元**  
 允許在 InfoObject 資料中使用小寫字元。  
  
 **儲存並啟用**  
 儲存並啟用新的 InfoObject。  
  
## <a name="data-type-options"></a>資料類型選項  
 **CHAR - 字元字串**  
 表示 InfoObject 包含字元資料。  
  
 **NUMC - 數值字串**  
 表示 InfoObject 包含數值資料。  
  
 **DATS - 日期 (YYYYMMDD)**  
 表示 InfoObject 包含日期資料。  
  
 **TIMS - 時間 (HHMMSS)**  
 表示 InfoObject 包含時間資料。  
  
 **長度**  
 輸入資料的長度。  
  
## <a name="text-options"></a>文字選項  
 **具有文字**  
 表示 InfoObject 包含文字。  
  
 **短文字**  
 表示 InfoObject 包含短文字。  
  
 **中長文字**  
 表示 InfoObject 包含中長文字。  
  
 **長文字**  
 表示 InfoObject 包含長文字。  
  
 **與文字語言相依**  
 表示文字具有語言相依性。  
  
 **與文字時間相依**  
 表示文字具有時間相依性。  
  
## <a name="attributes-section"></a>屬性區段  
 **[屬性]** 區段包含 InfoObject 的屬性清單，以及可讓您在清單中加入和移除屬性的選項。  
  
### <a name="attributes-list"></a>屬性清單  
 **[屬性]** 清單會顯示您所建立之 InfoObject 的屬性。 **[屬性]** 清單具有下列資料行標題：  
  
 **[InfoObject]**  
 檢視 InfoObject 的名稱。  
  
 **說明**  
 檢視 InfoObject 的描述。  
  
 **InfoObject 類型**  
 檢視 InfoObject 的類型。 下表列出類型的可能值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|CHA|特性|  
|KYF|關鍵數據|  
|UNI|單位|  
|TIM|時間特性|  
  
### <a name="attributes-options"></a>屬性選項  
 使用下列選項可以針對您所建立的 InfoObject 加入和移除屬性：  
  
 **[加入]**  
 加入現有的 InfoObject 做為屬性。  
  
 若要加入現有的 InfoObject，請按一下 [加入]，然後使用 **[查閱 InfoObject]** 對話方塊來尋找 InfoObject。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md)＞。  
  
 **[新增]**  
 加入新的 InfoObject 做為屬性。  
  
 若要建立並加入新的 InfoObject，請按一下 [新增]，然後使用 **[建立新的 InfoObject]** 對話方塊的新執行個體來建立新的 InfoObject。  
  
 **移除**  
 從 [屬性] 清單中移除選取的 InfoObject。  
  
## <a name="see-also"></a>另請參閱  
 [建立交易資料的 InfoCube](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [建立 InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [建立交易資料的 InfoSource](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [[建立主要資料的 InfoSource]](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
