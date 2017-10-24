---
title: "DataFactory 自訂 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 044e738c69113740290843f14f0b2c14500307e1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="datafactory-customization"></a>DataFactory 自訂
遠端資料服務 (RDS) 提供方法來輕鬆地在三層式用戶端/伺服器系統執行資料存取。 用戶端資料控制項指定遠端資料來源或連接字串上執行查詢的連接和命令字串參數和[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件參數來執行更新。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 參數會傳遞至伺服器的程式，可執行遠端資料來源上的資料存取作業。 RDS 提供呼叫的預設伺服器程式[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。 **RDSServer.DataFactory**物件會傳回任何**資料錄集**物件所產生的用戶端查詢。  
  
 不過， **RDSServer.DataFactory**限制為執行查詢和更新。 它無法連線或命令字串上執行任何驗證或處理。  
  
 使用 ADO 時，您可以指定**DataFactory**中另一種稱為伺服器程式搭配運作*處理常式*。 它們可用來存取資料來源之前，此處理常式可以修改用戶端連接和命令字串。 此外，此處理常式可以強制執行存取權限，控制用戶端讀取及寫入資料至資料來源的能力。  
  
 修改用戶端參數和存取權限的處理常式使用的參數被指定自訂檔案的區段中。  
  
 下列主題提供自訂的相關資訊**DataFactory**物件。  
  
-   [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [必要用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



