---
title: 自訂檔案連接 > 一節 |Microsoft 文件
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
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0835a305ce4e7c748c4b7a8c931a586f70d2bafa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="customization-file-connect-section"></a>自訂檔案連接 > 一節
此處理常式的預設行為是拒絕所有連線。 **連接**區段會指定該行為的例外狀況。 例如，如果所有**連接**區段已不存在或空的則預設無法建立任何連線。  
  
 **連接**區段只能包含：  
  
-   預設存取項目，指定預設的讀取和寫入這個連接上允許的作業。 如果區段中，沒有預設存取項目，將會忽略 > 一節。  
  
-   新的連接字串，它會取代用戶端連接字串。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 格式是預設存取項目：  
  
```  
  
Access=  
accessRight  
  
```  
  
 格式是取代連接字串項目：  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>備註  
  
|部分|Description|  
|----------|-----------------|  
|**連接**|常值字串，表示這是連接字串的項目。|  
|***connectionString***|字串，取代整個用戶端連接字串。|  
|**存取**|常值字串，表示這是存取項目。|  
|***accessRight***|其中一個的下列存取權限：<br /><br /> -   **NoAccess** -使用者無法存取資料來源。<br />-   **ReadOnly** — 使用者可以讀取的資料來源。<br />-   **ReadWrite** — 使用者可讀取或寫入至資料來源。|  
  
 如果您想要允許任何連線 （效果，請停用預設處理常式的行為），設定存取項目**連接預設**區段`Access=ReadWrite`，並刪除或標記為註解的任何其他**連接***識別碼*> 一節。  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案記錄檔 > 一節](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



