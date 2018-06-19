---
title: 在資料流程元件中將查詢參數對應至變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d33b3123c683ebeae45283c7b69058b7037ab18d
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334172"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>在資料流程元件中將查詢參數對應至變數
  將 OLE DB 來源設定為使用參數化查詢時，可以將參數對應至變數。  
  
 當 OLE DB 來源連接到資料來源時，會使用參數化查詢來篩選資料。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>將查詢參數對應至變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將 OLE DB 來源從 **[工具箱]** 拖曳到設計介面。  
  
4.  以滑鼠右鍵按一下 [OLE DB 來源]，然後按一下 [編輯]。  
  
5.  在 [OLE DB 來源編輯器] 中選取用來連接資料來源的 OLE DB 連線管理員，或按一下 [新增] 以建立新的 OLE DB 連線管理員。  
  
6.  為資料存取模式選取 [SQL 命令] 選項，然後在 [SQL 命令文字] 窗格中輸入參數化查詢。  
  
7.  按一下 **[參數]**。  
  
8.  在 [設定查詢參數] 對話方塊中，將 [參數] 清單中的每個參數對應至 [變數] 清單中的變數，或按一下 [\<新增變數>] 來建立新變數。 按一下 [確定] 。  
  
    > [!NOTE]  
    >  只有封裝、「Foreach 迴圈」之類的父容器或包含資料流程元件之「資料流程」工作等範圍內的系統變數和使用者自訂變數才可用於對應。 變數的資料類型必須與指派參數之 WHERE 子句中的資料行相容。  
  
9. 您可以按一下 [預覽]，以檢視查詢所傳回之最多 200 個資料列的資料。  
  
10. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 來源](../../integration-services/data-flow/ole-db-source.md)   
 [查閱轉換](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
