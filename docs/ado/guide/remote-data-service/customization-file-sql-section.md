---
title: 自訂檔案 SQL 區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6163a5b5fd0999e17e17961639e0a1fee3e8fa4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922789"
---
# <a name="customization-file-sql-section"></a>自訂檔案 SQL 區段
**Sql**區段可以包含新的 SQL 字串，它會取代用戶端命令字串。 如果沒有區段中的 SQL 字串，將會忽略一節。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字串可能*參數化*。 也就是中的參數**sql**區段 SQL 字串 (指定的 '？ ' 字元) 中對應的引數所能取代*識別碼*用戶端的命令字串中 (所指定以逗號分隔清單在括號中）。 識別項和引數清單的行為類似函式呼叫。  
  
 比方說，假設用戶端命令字串很`"CustomerByID(4)"`，SQL 區段標頭`[SQL CustomerByID]`，且新的 SQL 區段字串`"SELECT * FROM Customers WHERE CustomerID = ?".`處理常式將會產生`"SELECT * FROM Customers WHERE CustomerID = 4"`和使用該字串，來查詢資料來源。  
  
 如果新的 SQL 陳述式為 null 的字串 ("")，則會忽略一節。  
  
 如果新的 SQL 陳述式字串不是有效的然後執行陳述式會失敗。 用戶端會有效地略過該參數。 您可以執行刻意為 「 關閉 」 所有的用戶端 SQL 命令藉由指定：  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>語法  
 取代 SQL 字串項目屬於表單：  
  
 **SQL=**    
 ***sqlString***  
  
|部分|描述|  
|----------|-----------------|  
|**SQL**|常值字串，表示這是 SQL 區段項目。|  
|***sqlString***|SQL 字串，它會取代用戶端的字串。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


