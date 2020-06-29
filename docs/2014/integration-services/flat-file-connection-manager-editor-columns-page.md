---
title: 一般檔案連線管理員編輯器（資料行頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.columns.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 40ce7537-abd0-4973-97fd-6ccb90fddfa0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c1b2a60f82e354513d25003b035bfbb689858107
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425665"
---
# <a name="flat-file-connection-manager-editor-columns-page"></a>一般檔案連接管理員編輯器 (資料行頁面)
  使用 **[一般檔案連接管理員編輯器]** 對話方塊的 **[資料行]** 頁面來指定資料列和資料行資訊，以及預覽檔案。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](connection-manager/file-connection-manager.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
## <a name="flat-file-format-dynamic-options"></a>一般檔案格式動態選項  
  
### <a name="format--delimited"></a>格式 = 使用分隔符號  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是以歸位字元和換行字元的組合分隔。|  
|**符**|資料列是以歸位字元分隔。|  
|**分行符號**|資料列是以換行字元分隔。|  
|**分號 {;}**|資料列是以分號分隔。|  
|**冒號 {:}**|資料列是以冒號分隔。|  
|**千{,}**|資料列是以逗號分隔。|  
|**定位字元 {t}**|資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料列是以分隔號分隔。|  
  
 **資料行分隔符號**  
 從可用的資料行分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是以歸位字元和換行字元的組合分隔。|  
|**符**|資料行是以歸位字元分隔。|  
|**分行符號**|資料行是以換行字元分隔。|  
|**分號 {;}**|資料行是以分號分隔。|  
|**冒號 {:}**|資料行是以冒號分隔。|  
|**千{,}**|資料行是以逗號分隔。|  
|**定位字元 {t}**|資料行是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料行是以分隔號分隔。|  
  
 **重新整理**  
 按一下 [重新整理]****，即可檢視變更要略過之分隔符號的影響。 僅在您已變更其他連接選項之後，才會看見此按鈕。  
  
 **預覽資料列**  
 檢視一般檔案中的範例資料，使用選取的選項將資料分為資料行和資料列。  
  
 **重設資料行**  
 按一下 [重設資料行]****，即可將原始資料行以外的資料行全部移除。  
  
### <a name="format--fixed-width"></a>格式 = 固定寬度  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直紅色資料列標記，即可調整資料列的寬度；而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列寬度**  
 為個別資料行加入分隔符號之前，請先指定資料列的長度。 或者，在預覽視窗中拖曳垂直紅線來標示資料列結尾。 資料列寬度值會自動更新。  
  
 **重設資料行**  
 按一下 [重設資料行]****，即可將原始資料行以外的資料行全部移除。  
  
### <a name="format--ragged-right"></a>格式 = 不齊右  
  
> [!NOTE]  
>  不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。  
  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直紅色資料列標記，即可調整資料列的寬度；而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是以歸位字元和換行字元的組合分隔。|  
|**符**|資料列是以歸位字元分隔。|  
|**分行符號**|資料列是以換行字元分隔。|  
|**分號 {;}**|資料列是以分號分隔。|  
|**冒號 {:}**|資料列是以冒號分隔。|  
|**千{,}**|資料列是以逗號分隔。|  
|**定位字元 {t}**|資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料列是以分隔號分隔。|  
  
 **重設資料行**  
 按一下 [重設資料行]****，即可將原始資料行以外的資料行全部移除。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [一般檔案連線管理員編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [一般檔案連線管理員編輯器 &#40;Advanced Page&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
