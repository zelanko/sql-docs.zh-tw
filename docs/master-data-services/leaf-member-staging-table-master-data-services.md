---
title: "Leaf Member Staging Table (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "members staging table [Master Data Services]"
  - "資料庫 [Master Data Services], 成員暫存表格"
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Leaf Member Staging Table (Master Data Services)
  使用暫存資料表 (stg.name_Leaf) 中的分葉成員 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 來建立、 更新、 停用，以及刪除分葉成員的資料庫。 您也可以用它來更新分葉成員的屬性值。  
  
##  <a name="TableColumns"></a> 資料表資料行  
 下表說明分葉暫存資料表中各欄位的用途。  
  
|資料行名稱|描述|值|  
|-----------------|-----------------|------------|  
|**ID**|自動指派的識別碼。|請勿在此欄位中輸入值。 如果尚未處理批次，這個欄位是空白。|  
|**ImportType**<br /><br /> Required|決定在暫存資料符合 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中既存的資料時，該怎麼做。|**0**：建立新成員。 將現有的 MDS 資料取代為暫存資料，但唯有在暫存資料不是 NULL 的情況下。 系統會忽略 NULL 值。 若要將字串屬性值變更為 NULL，請將它設定為 **~NULL~**。 若要變更數字的屬性值為 NULL，將它設定為 **-98765432101234567890**。 若要變更的日期時間屬性值為 NULL，將它設定為 **5555-11-22T12:34:56**。<br /><br /> **1**：只建立新成員。 對現有 MDS 資料的任何更新都將失敗。<br /><br /> **2**：建立新的成員。 將現有的 MDS 資料取代為暫存資料。 如果您匯入 NULL 值，它們會覆寫現有的 MDS 值。<br /><br /> **3**：依據字碼值停用成員。 將會維護所有屬性、階層和集合成員資格，以及交易，但已無法在使用者介面中使用。 如果成員當做另一個成員的網域屬性值使用，則停用將會失敗。 請參閱 **ImportType5** 如需替代方法。<br /><br /> **4**：依據字碼值，永久刪除成員。 將會永久刪除所有屬性、階層和集合成員資格，以及交易。 如果成員當做另一個成員的網域屬性值使用，則刪除將會失敗。 請參閱 **ImportType6** 如需替代方法。<br /><br /> **5**：依據 **[字碼]** 值停用成員。 將會維護所有屬性、階層和集合成員資格，以及交易，但已無法在使用者介面中使用。 如果成員當做其他成員的網域屬性值使用，則相關的值將會設為 NULL。 ImportType 5 僅適用於分葉成員。<br /><br /> **6**：依據 **[字碼]** 值，永久刪除成員。 將會永久刪除所有屬性、階層和集合成員資格，以及交易。 如果成員當做其他成員的網域屬性值使用，則相關的值將會設為 NULL。 ImportType 6 僅適用於分葉成員。|  
|**ImportStatus_ID**<br /><br /> Required|匯入程序的狀態。|**0**：您用來指定記錄已備妥，可供暫存。<br /><br /> **1**：自動指派，表示記錄的暫存處理序已成功。<br /><br /> **2**：自動指派，表示記錄的暫存處理序已失敗。|  
|**Batch_ID**<br /><br /> 只有 Web 服務需要|自動指派的識別碼，可用來將暫存的記錄分組。 批次中的所有成員都會被指派這個識別碼，這個識別碼會顯示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面的 **[識別碼]** 欄中。|如果尚未處理批次，這個欄位是空白。|  
|**BatchTag**<br /><br /> 必要項，只有 Web 服務不需要|批次的唯一名稱 (最多 50 個字元)。||  
|**ErrorCode**|顯示錯誤碼。 所有記錄 **ImportStatus_ID** 的 **2**, ，請參閱 [暫存處理序錯誤 & #40。Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)。||  
|**程式碼**<br /><br /> 必要項目，除了當程式碼會自動產生 **ImportType1** 或 **2**; 請參閱 [自動程式碼建立 & #40。Master Data Services & #41;](../master-data-services/automatic-code-creation-master-data-services.md) 如需詳細資訊|成員的唯一代碼。||  
|**名稱**<br /><br /> 選擇性|成員的名稱。||  
|**NewCode**|唯有在您要變更成員代碼時才使用。||  
|\< 屬性名稱>|實體中的每個屬性都有一個資料行存在。 將其搭配 **ImportType** **0** 或 **2**使用。 對於自由格式屬性，指定屬性的新文字或字串值。 對於網域屬性，指定將成為屬性之成員的代碼。 對於連結屬性，URL 的開頭必須 **http://**。<br /><br /> 注意：您無法暫存檔案屬性。||  
  
## 另請參閱  
 [概觀︰ 從資料表 & #40; 匯入資料Master Data Services & #41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [檢視暫存 & #40; 期間發生的錯誤Master Data Services & #41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [暫存處理序錯誤 & #40。Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  