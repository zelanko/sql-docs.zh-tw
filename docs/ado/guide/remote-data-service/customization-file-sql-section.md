---
title: 自訂檔案 SQL > 一節 |Microsoft 文件
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
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6294ab601f527527cf69ca017e3643dfe98a1336
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="customization-file-sql-section"></a>自訂檔案 SQL > 一節
**Sql**區段只能包含新的 SQL 字串，取代用戶端的命令字串。 如果沒有 SQL 字串的區段中，將會忽略 > 一節。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 可能是新的 SQL 字串*參數化*。 也就是說，參數在**sql**區段 SQL 字串 (所指定 '？ ' 字元) 中對應的引數所能取代*識別碼*用戶端命令字串中 (所指定以逗號分隔清單括號括住）。 識別項和引數清單的行為與函式呼叫。  
  
 例如，假設用戶端命令字串很`"CustomerByID(4)"`，SQL 區段標頭是`[SQL CustomerByID]`，且新的 SQL 區段字串`"SELECT * FROM Customers WHERE CustomerID = ?".`的處理常式將會產生`"SELECT * FROM Customers WHERE CustomerID = 4"`並使用該字串，來查詢資料來源。  
  
 如果新的 SQL 陳述式為 null 的字串 ("")，則會忽略 > 一節。  
  
 如果新的 SQL 陳述式字串不是有效的則執行陳述式會失敗。 用戶端參數有效地被忽略。 您可以執行此刻意 「 關閉 」 所有用戶端 SQL 命令藉由指定：  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>語法  
 格式是取代 SQL 字串的項目：  
  
 **SQL=**   
 ***sqlString***  
  
|部分|Description|  
|----------|-----------------|  
|**SQL**|常值字串，表示這是 SQL 區段項目。|  
|***sqlString***|SQL 字串，取代用戶端的字串。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄檔 > 一節](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


