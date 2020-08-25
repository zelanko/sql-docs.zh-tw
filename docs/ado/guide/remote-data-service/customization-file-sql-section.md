---
description: 自訂檔案 SQL 區段
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7be4aaa2a92de4f778ee69422b97ceb169411c10
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759822"
---
# <a name="customization-file-sql-section"></a>自訂檔案 SQL 區段
**Sql**區段可以包含取代用戶端命令字串的新 sql 字串。 如果區段中沒有 SQL 字串，則會忽略區段。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字串可能已 *參數化*。 也就是說， **sql** 區段 sql 字串中的參數 (由 '？ ' 字元指定) 可由用戶端命令字串中 *識別碼* 內的對應引數取代，) 中以逗號分隔的清單指定 (。 識別碼和引數清單的行為就像函式呼叫一樣。  
  
 例如，假設用戶端命令字串為 `"CustomerByID(4)"` ，sql 區段標頭為 `[SQL CustomerByID]` ，而且新的 sql 區段字串是 `"SELECT * FROM Customers WHERE CustomerID = ?".` 處理常式將會產生 `"SELECT * FROM Customers WHERE CustomerID = 4"` 並使用該字串來查詢資料來源。  
  
 如果新的 SQL 語句是 null 字串 ( "" ) ，則會忽略區段。  
  
 如果新的 SQL 語句字串無效，語句的執行將會失敗。 用戶端參數實際上會被忽略。 您可以藉由指定下列命令，刻意「關閉」所有用戶端 SQL 命令：  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>語法  
 取代的 SQL 字串專案的形式如下：  
  
 **SQL =**   
 ***sqlString***  
  
|部分|描述|  
|----------|-----------------|  
|**SQL**|表示這是 SQL 區段專案的常值字串。|  
|***sqlString***|取代用戶端字串的 SQL 字串。|  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](./customization-file-connect-section.md)   
 [自訂檔案記錄區段](./customization-file-logs-section.md)   
 [自訂檔案 UserList 區段](./customization-file-userlist-section.md)   
 [DataFactory 自訂](./datafactory-customization.md)   
 [必要的用戶端設定](./required-client-settings.md)   
 [瞭解自訂檔案](./understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)