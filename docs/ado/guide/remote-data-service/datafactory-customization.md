---
title: DataFactory 自訂 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdc406778bea0d6355e747998d2517b841fc17b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922774"
---
# <a name="datafactory-customization"></a>DataFactory 自訂
遠端資料服務 (RDS) 可用來輕鬆地在三層式用戶端/伺服器系統執行資料存取。 用戶端資料控制項指定遠端資料來源或連接字串上執行查詢的連接和命令字串參數和[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件執行更新的參數。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 參數會傳遞至伺服器程式中，它會執行的遠端資料來源的資料存取作業。 RDS 提供預設伺服器程式呼叫[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。 **RDSServer.DataFactory**物件會傳回任何**資料錄集**查詢，以用戶端所產生的物件。  
  
 不過， **RDSServer.DataFactory**僅限於執行查詢和更新。 它無法連接或命令字串上執行任何驗證或處理。  
  
 使用 ADO 時，您可以指定**DataFactory**搭配另一種伺服器程式呼叫工作*處理常式*。 它們用來存取資料來源之前，處理常式可以修改用戶端連接和命令字串。 此外，這個處理常式可以強制執行控管的能力，來讀取和寫入資料至資料來源的用戶端的存取權。  
  
 自訂檔案的區段中指定的參數處理常式會使用修改用戶端參數和存取權限。  
  
 下列主題提供自訂的相關資訊**DataFactory**物件。  
  
-   [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [自訂檔案 Logs 區段](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [必要用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


