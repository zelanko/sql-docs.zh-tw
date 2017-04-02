---
title: "一般檔案連接管理員編輯器 (進階頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ffileconnection.columnproperties.f1"
helpviewer_keywords: 
  - "一般檔案連接管理員編輯器"
ms.assetid: 58aa3dee-4774-4e0b-a956-96d199be4c3a
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# 一般檔案連接管理員編輯器 (進階頁面)
  您可以使用 [一般檔案連線管理員編輯器] 對話方塊的 [進階] 頁面設定屬性，以指定 Integration Services 讀取及寫入一般檔案的方式。 您可以變更一般檔案中的資料行名稱，並設定屬性以包含檔案中每個資料行的資料類型和分隔符號。  
  
 字串資料行的長度預設為 50 個字元。 您可以調整這些資料行的長度，以避免截斷資料或資料行寬度過大。 您也可更新其他中繼資料，以啟用與目的地資料行的相容性。 例如，您可能會將只包含整數資料之資料行的資料類型變更成數值資料類型 (例如 DT_I2)。 您可以手動進行這些修改，也可以按一下 [選取類型] 按鈕，使用 [建議資料行類型] 對話方塊評估範例資料，並自動為您進行其中某些變更。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)＞。  
  
## 選項。  
 **連接管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接管理員。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接管理員。 最佳作法是以其用途描述連接管理員，使封裝可以自我記錄並易於維護。  
  
 **設定每一個資料行的屬性**  
 請在左窗格中選取一個資料行以便在右窗格中檢視它的屬性。 請參閱下表以了解資料類型屬性的描述。 部分列出的屬性，只能在某些一般檔案格式中設定。  
  
|屬性|說明|  
|--------------|-----------------|  
|**ColumnType**|代表資料行是否為分隔的、固定寬度或不齊右。 此屬性是唯讀的。 不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。|  
|**OutputColumnWidth**|指定儲存為位元組計數的值；針對 Unicode 檔案，此值將對應至字元計數。 在資料流程工作中，這個值將用來替一般檔案來源設定輸出資料行寬度。 在物件模型中，這個屬性的名稱為 MaximumWidth。|  
|**DataType**|從可用的資料類型清單中選取。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。|  
|**TextQualified**|指出文字資料是否會由文字限定詞字元 (例如引號字元) 括住。<br /><br /> True：一般檔案中的文字資料是限定的。 False：一般檔案中的文字資料是非限定的。|  
|**名稱**|提供描述性資料行名稱。 如果未輸入名稱，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動以 Column 0、Column 1 等等的格式建立名稱。|  
|**DataScale**|指定數值資料的小數位數。 小數位數是指小數位數的數目。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。|  
|**ColumnDelimiter**|從可用的資料行分隔符號清單中選取。 請選擇不太可能會在文字中出現的分隔符號。 固定寬度資料行將忽略這個值。<br /><br /> **{CR}{LF}**： 資料行是以歸位字元和換行字元的組合分隔。<br /><br /> **{CR}**： 資料行是以歸位字元分隔。<br /><br /> **{LF}**： 資料行是以換行字元分隔。<br /><br /> **分號 {;}**： 資料行是以分號分隔。<br /><br /> **冒號 {:}**： 資料行是以冒號分隔。<br /><br /> **逗號 {,}**： 資料行是以逗號分隔。<br /><br /> **定位字元 {t}**： 資料行是以定位字元分隔。<br /><br /> **分隔號 {&#124;}**： 資料行是以分隔號分隔。|  
|**DataPrecision**|指定數值資料的有效位數。 有效位數是指位數的數目。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。|  
|**InputColumnWidth**|指定將儲存為位元組計數的值；針對 Unicode 檔案，這將會顯示為字元計數。 分隔資料行將忽略這個值。<br /><br /> **注意**︰在物件模型中，這個屬性的名稱為 ColumnWidth。|  
  
 **新增**  
 按一下 [新增] 來加入新的資料行。 依預設，[新增] 按鈕會在清單結尾加入新的資料行。 此按鈕還有下列選項，可以在下拉式清單中使用。  
  
|Value|說明|  
|-----------|-----------------|  
|**加入資料行**|在清單結尾加入新資料行。|  
|**插在前面**|在選取的資料行之前插入新資料行。|  
|**插在後面**|在選取的資料行之後插入新資料行。|  
  
 **Delete**  
 選取資料行，然後按一下 [刪除] 將其移除。  
  
 **建議類型**  
 使用 [建議資料行類型] 對話方塊，評估檔案中的範例資料，並取得對每個資料行之資料類型和長度的建議。 如需詳細資訊，請參閱[建議資料行類型對話方塊 UI 參考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)   
 [一般檔案連線管理員編輯器 &#40;資料行頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  