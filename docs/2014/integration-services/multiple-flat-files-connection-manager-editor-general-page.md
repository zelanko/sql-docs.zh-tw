---
title: 多個一般檔案連接管理員編輯器 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3c7af9641ffc033c2c7173eaf74884700de7a3ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176438"
---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>多個一般檔案連線管理員編輯器 (一般頁面)
  使用 **[多個一般檔案連線管理員編輯器]** 對話方塊的 **[一般]** 頁面，即可選取一組具有相同資料格式的檔案，並指定其資料格式。 多個一般檔案連接，可以讓封裝連接到一組具有相同格式的文字檔。  
  
 若要深入了解多個一般檔案連線管理員，請參閱＜ [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)＞。  
  
## <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的多個一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **檔案名稱**  
 輸入路徑和檔案名稱，以便於多個一般檔案連接中使用。 您可以使用萬用字元來指定多個檔案，例如 "C:\\\*.txt"，或者使用分隔號 (|) 來分隔多個檔案名稱。 所有檔案必須有相同的資料格式。  
  
 **瀏覽**  
 瀏覽檔案名稱，以便於多個一般檔案連接中使用。 您可以選取多個檔案。 所有檔案必須有相同的資料格式。  
  
 **地區設定**  
 指定地區，以提供排序以及時間和日期的轉換資訊。  
  
 **Unicode**  
 指出是否使用 Unicode。 使用 Unicode 即無需指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **格式**  
 指出是要使用分隔符號、固定寬度或不齊右的格式。 所有檔案必須有相同的資料格式。  
  
|值|描述|  
|-----------|-----------------|  
|使用分隔符號|資料行是以分隔符號隔開，分隔符號是在 **[資料行]** 頁面上指定的。|  
|固定寬度|資料行具有固定寬度，由 **[資料行]** 頁面上的拖曳標記線所指定。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有在 **[資料行]** 頁面上所指定之固定寬度的檔案。|  
  
 **文字定位項**  
 指定要使用的文字限定詞。 例如，您可以指定文字必須加上引號。  
  
 **標頭資料列分隔符號**  
 從標頭資料列的分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|標頭資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|標頭資料列是以歸位字元分隔。|  
|**{LF}**|標頭資料列是以換行字元分隔。|  
|**分號 {;}**|標頭資料列是以分號分隔。|  
|**冒號 {:}**|標頭資料列是以冒號分隔。|  
|**逗號 {,}**|標頭資料列是以逗號分隔。|  
|**定位字元 {t}**|標頭資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|標頭資料列是以分隔號 (&#124;) 分隔。|  
  
 **略過的標頭資料列數**  
 指定要略過的標頭列數 (如果有的話)。  
  
 **第一個資料列的資料行名稱**  
 指出在第一個資料列中，是否為資料行名稱或需要提供資料行名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [多個一般檔案連接管理員編輯器&#40;資料行頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [多個一般檔案連接管理員編輯器&#40;進階頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [多個一般檔案連接管理員編輯器&#40;預覽頁面&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
