---
title: 一般檔案連線管理員編輯器（一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0f4387b3311c4b2157ba202890c2a190e83e7ad5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967098"
---
# <a name="flat-file-connection-manager-editor-general-page"></a>一般檔案連接管理員編輯器 (一般頁面)
  使用 **[一般檔案連接管理員編輯器]** 對話方塊的 **[一般]** 頁面，來選取檔案和資料格式。 一般檔案連接可以讓封裝連接到文字檔。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](connection-manager/file-connection-manager.md)＞。  
  
## <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **檔案名稱**  
 輸入在一般檔案連接中要使用的路徑和檔案名稱。  
  
 **瀏覽**  
 尋找在一般檔案連接中要使用的檔案名稱。  
  
 **Locale**  
 指定地區設定以提供排序以及日期和時間格式的特定語言資訊。  
  
 **Unicode**  
 指出是否使用 Unicode。 如果使用 Unicode，您就無法指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **[格式]**  
 指出檔案是要使用分隔符號、固定寬度或不齊右的格式。  
  
|值|描述|  
|-----------|-----------------|  
|Delimited (分隔檔)|資料行是以分隔符號隔開，分隔符號是在 **[資料行]** 頁面上指定的。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。|  
  
 **文字定位項**  
 指定要使用的文字限定詞。 例如，您可以指定文字欄位加上引號。  
  
> [!NOTE]  
>  選取文字限定詞之後，就無法重新選取 [無]**** 選項。 輸入 **None** 即可取消選取文字限定詞。  
  
 **標頭資料列分隔符號**  
 從標頭資料列的分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|標頭資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|標頭資料列是以歸位字元分隔。|  
|**分行符號**|標頭資料列是以換行字元分隔。|  
|**分號 {;}**|標頭資料列是以分號分隔。|  
|**冒號 {:}**|標頭資料列是以冒號分隔。|  
|**千{,}**|標頭資料列是以逗號分隔。|  
|**定位字元 {t}**|標頭資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|標頭資料列是以分隔號 (&#124;) 分隔。|  
  
 **略過的標頭資料列數**  
 指定要略過的標頭資料列數或初始資料列數 (如果有的話)。  
  
 **第一個資料列中的資料行名稱**  
 指出在第一個資料列中，是否為資料行名稱或需要提供資料行名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [一般檔案連接管理員編輯器 &#40;資料行] 頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [一般檔案連線管理員編輯器 &#40;Advanced Page&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
