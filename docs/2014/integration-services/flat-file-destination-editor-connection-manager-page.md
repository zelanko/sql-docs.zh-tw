---
title: 一般檔案目的地編輯器（連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c7d2c37e38386f7e46c1b8a0800d45dfc0b9b0dd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967076"
---
# <a name="flat-file-destination-editor-connection-manager-page"></a>一般檔案目的地編輯器 (連接管理員頁面)
  使用 [一般檔案目的地編輯器]**** 對話方塊的 [連線管理員]**** 頁面，來選取目的地的一般檔案連接，以及指定是否要覆寫或附加至現有的目的地檔案。 一般檔案目的地會將資料寫入文字檔。 此文字檔的格式可以是分隔、固定寬度、固定寬度且具有資料列分隔符號或不齊右格式。  
  
 若要深入了解一般檔案目的地，請參閱 [一般檔案目的地](data-flow/flat-file-destination.md)。  
  
## <a name="options"></a>選項。  
 **一般檔案連線管理員**  
 使用清單方塊選取現有的連線管理員，或按一下 [新增]**** 建立新的連接。  
  
 **新增**  
 使用 [一般檔案格式]**** 與 [一般檔案連線管理員編輯器]**** 對話方塊來建立新的連接。  
  
 除了標準一般檔案格式的 [使用分隔符號]、[固定寬度] 和 [不齊右] 等選項之外，[一般檔案格式]**** 對話方塊還有第四個選項 [有資料列分隔符號的固定寬度]****。 這個選項代表不齊右格式的特殊狀況， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會加入虛擬資料行當做最後資料行。 這個虛擬資料行可確保最終資料行有固定寬度。  
  
 [有資料列分隔符號的固定寬度]**** 選項不會出現在 [一般檔案連線管理員編輯器]**** 中。 必要時，您可以在編輯器中模擬這個選項。 若要模擬這個選項，請在 [一般檔案連線管理員編輯器]**** 的 [一般]**** 頁面上，針對 [格式]**** 選取 [不齊右]****。 然後在編輯器的 [進階]**** 頁面上，加入新的虛擬資料行當做最後資料行。  
  
 **覆寫檔案中的資料**  
 指出是要覆寫現有的檔案，還是將資料附加至檔案中。  
  
 **標頭**  
 在寫入任何資料之前，輸入要插入檔案中的文字區塊。 使用此選項來包含其他資訊，例如資料行標題。  
  
 **預覽**  
 使用 [資料檢視]**** 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [一般檔案目的地編輯器 &#40;對應頁面&#41;](../../2014/integration-services/flat-file-destination-editor-mappings-page.md)  
  
  
