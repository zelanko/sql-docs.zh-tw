---
title: "指令碼轉換編輯器 (指令碼頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.scriptcomponent.script.f1"
helpviewer_keywords: 
  - "指令碼轉換編輯器"
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# 指令碼轉換編輯器 (指令碼頁面)
  使用 **[指令碼轉換編輯器]** 對話方塊的 **[指令碼]** 索引標籤，來指定指令碼和相關的屬性。  
  
 若要深入了解指令碼元件，請參閱＜ [Script Component](../../../integration-services/data-flow/transformations/script-component.md) ＞和＜ [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)＞。 若要了解如何以程式設計方式編寫指令碼元件，請參閱＜ [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)＞。  
  
## 選項。  
 **屬性**  
 檢視和修改指令碼轉換的屬性。 顯示的許多屬性是唯讀的。 您可以修改下列屬性：  
  
|Value|說明|  
|-----------|-----------------|  
|**說明**|以其用途來描述指令碼轉換。|  
|**LocaleID**|指定地區設定以提供排序和日期和時間轉換的特定區域資訊。|  
|**名稱**|輸入元件的描述性名稱。|  
|**ValidateExternalMetadata**|指出指令碼轉換在設計階段是否對外部資料來源驗證資料行中繼資料。 **false** 的值將會延遲到執行時間才驗證。|  
|**ReadOnlyVariables**|輸入以逗號分隔的變數清單，以供指令碼轉換進行唯讀存取。<br /><br /> 注意：變數名稱會區分大小寫。|  
|**ReadWriteVariables**|輸入以逗號分隔的變數清單，以供指令碼轉換進行可讀寫存取。<br /><br /> 注意：變數名稱會區分大小寫。|  
|**ScriptLanguage**|選取指令碼元件所要使用的指令碼語言。<br /><br /> 若要為指令碼元件和指令碼工作設定預設指令碼語言，請使用 **[選項]** 對話方塊上 **[一般]** 頁面上的 **[指令碼語言]** 選項。|  
|**UserComponentTypeName**|指定支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 基礎結構的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> 類別和 **Microsoft.SqlServer.TxScript** 組件。|  
  
 **編輯指令碼**  
 使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 來建立或修改指令碼。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [選取指令碼元件類型](../../../integration-services/data-flow/transformations/select-script-component-type.md)   
 [指令碼轉換編輯器 &#40;輸入資料行頁面&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)   
 [指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)   
 [指令碼轉換編輯器 &#40;連接管理員頁面&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)   
 [額外的指令碼元件範例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  