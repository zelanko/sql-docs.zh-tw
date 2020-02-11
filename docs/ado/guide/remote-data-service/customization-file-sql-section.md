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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922789"
---
# <a name="customization-file-sql-section"></a>自訂檔案 SQL 區段
**Sql**區段可以包含取代用戶端命令字串的新 sql 字串。 如果區段中沒有 SQL 字串，將會忽略區段。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字串可能已*參數化*。 也就是**sql**區段 sql 字串（由 '？ ' 字元指定）中的參數，可以由用戶端命令字串中的*識別碼*（以括弧括住的逗號分隔清單所指定）中的對應引數取代。 [識別碼] 和 [引數] 清單的行為與函式呼叫類似。  
  
 例如，假設用戶端`"CustomerByID(4)"`命令字串是，sql 區段標頭是`[SQL CustomerByID]`，而新的 Sql 區段字串是`"SELECT * FROM Customers WHERE CustomerID = ?".`處理常式將會產生`"SELECT * FROM Customers WHERE CustomerID = 4"`並使用該字串來查詢資料來源。  
  
 如果新的 SQL 語句是 null 字串（""），則會忽略區段。  
  
 如果新的 SQL 語句字串無效，則語句的執行將會失敗。 會有效忽略用戶端參數。 您可以藉由指定下列方式，故意「關閉」所有用戶端 SQL 命令：  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>語法  
 取代 SQL 字串專案的格式如下：  
  
 **SQL =**   
 ***sqlString***  
  
|部分|描述|  
|----------|-----------------|  
|**SERVER**|表示這是 SQL 區段專案的常值字串。|  
|***sqlString***|取代用戶端字串的 SQL 字串。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案記錄區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [瞭解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


