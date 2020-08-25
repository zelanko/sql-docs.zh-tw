---
description: DataFactory 自訂
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c34ae14feda7c0a6847d638f35bf84c6b9cd0fd5
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759802"
---
# <a name="datafactory-customization"></a>DataFactory 自訂
遠端資料服務 (RDS) 可讓您輕鬆地在三層用戶端/伺服器系統中執行資料存取。 用戶端資料控制項會指定連接和命令字串參數，以對遠端資料源執行查詢，或是使用連接字串和 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件參數來執行更新。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 參數會傳遞至伺服器程式，以在遠端資料源上執行資料存取作業。 RDS 提供預設的伺服器程式，稱為 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件。 **RDSServer. DataFactory**物件會將查詢所產生的任何**記錄集**物件傳回給用戶端。  
  
 不過， **RDSServer DataFactory** 僅限於執行查詢和更新。 它無法對連接或命令字串執行任何驗證或處理。  
  
 您可以使用 ADO 來指定 **DataFactory** 與另一種稱為 *處理*程式的伺服器程式搭配使用。 處理常式可以在用來存取資料來源之前修改用戶端連接和命令字串。 此外，處理常式也可以強制執行存取權限，以管理用戶端讀取和寫入資料來源的能力。  
  
 處理常式用來修改用戶端參數和存取權限的參數是在自訂檔的區段中指定。  
  
 下列主題提供自訂 **DataFactory** 物件的詳細資訊。  
  
-   [了解自訂檔案](./understanding-the-customization-file.md)  
  
-   [自訂檔案 Connect 區段](./customization-file-connect-section.md)  
  
-   [自訂檔案 SQL 區段](./customization-file-sql-section.md)  
  
-   [自訂檔案 UserList 區段](./customization-file-userlist-section.md)  
  
-   [自訂檔案 Logs 區段](./customization-file-logs-section.md)  
  
-   [必要用戶端設定](./required-client-settings.md)  
  
-   [撰寫您自己的自訂處理常式](./writing-your-own-customized-handler.md)