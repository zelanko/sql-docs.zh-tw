---
title: 了解的自訂檔案 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e80dc4615803b840f285033bd75186561dc21ddf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-customization-file"></a>了解自訂檔
方括號所組成的自訂檔案中的每個區段標頭 (**[]**) 包含型別和參數。 四個區段類型以常值字串**連接**， **sql**， **userlist**，或**記錄**。 常值字串、 預設值，指定使用者的識別項，或不提供參數。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每個區段會標示下列區段標頭的其中一個：  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 區段標頭有下列的部分。  
  
|部分|Description|  
|----------|-----------------|  
|**connect**|修改連接字串常值字串。|  
|**sql**|修改命令字串常值字串。|  
|**userlist**|常值字串，以修改特定使用者的存取權限。|  
|**logs**|常值字串，指定記錄作業的錯誤記錄檔。|  
|**default**|如果指定或找到沒有識別項會使用常值字串。|  
|*identifier*|比對字串中的字串**連接**或**命令**字串。<br /><br /> -使用此區段，如果區段標頭包含**連接**，且連接字串中找到的識別項字串。<br />-使用此區段，如果區段標頭包含**sql**和命令字串中找到的識別項字串。<br />-使用此區段，如果區段標頭包含**userlist**和識別項字串符合**連接**區段識別項。|  
  
 **DataFactory**呼叫處理常式，並傳遞用戶端的參數。 此處理常式中搜尋符合適當的區段標頭中的識別項的用戶端參數中的整個字串。 如果找到相符項目，該區段的內容會套用至用戶端參數。  
  
 在下列情況下，請使用特定區段：  
  
-   A**連接**區段的用戶端的值部分連接字串關鍵字，如果使用"**資料來源 = * * * 值*"，符合**連接**區段識別項 *.*  
  
-   **Sql**區段用戶端命令字串包含符合的字串，如果**sql**區段識別項。  
  
-   A**連接**或**sql**如果沒有相符識別項，會使用預設參數區段。  
  
-   A **userlist**區段用如果**userlist**區段識別項相符項目**連接**區段識別項。 如果沒有相符項目，內容**userlist**區段會套用至所控管連接**連接**> 一節。  
  
-   如果連接或命令字串中的字串不符合任何識別碼**連接**或**sql**區段標頭，而且沒有任何**連接**或**sql**區段標頭的預設參數，則用戶端字串會使用不需要修改。  
  
-   **記錄**區段用每當**DataFactory**在作業。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄檔 > 一節](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)




















