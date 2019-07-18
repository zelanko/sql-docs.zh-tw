---
title: Transact-SQL 中的 OLE Automation 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], OLE Automation
- batches [SQL Server], OLE Automation
- OLE Automation [SQL Server]
- OLE Automation [SQL Server], about OLE Automation
ms.assetid: a887d956-4cd0-400a-aa96-00d7abd7c44b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06913c27af89657aef5a0a5397cd77a1ee025299
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211859"
---
# <a name="ole-automation-objects-in-transact-sql"></a>Transact-SQL 中的 OLE Automation 物件
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 包含多個系統預存程序，可讓您在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、預存程序與觸發程序中參考 OLE Automation 物件。 這些系統預存程序以擴充預存程序來執行，而透過預存程序執行的 OLE Automation 物件在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體的位址空間內的執行方式與擴充預存程序的執行方式相同。  
  
 OLE Automation 預存程序可讓 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次參考 SQL-DMO 物件和自訂 OLE Automation 物件，例如公開 **IDispatch** 介面的物件。 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 所建立的自訂、內含式 OLE 伺服器必須具有 **On Error GoTo** 和 **On Error GoTo** 副程式的錯誤處理常式 (請使用 **On Error GoTo** 陳述式來指定此錯誤處理常式)。 **Class_Initialize** 與 **Class_Terminate** 副程式中的未處理錯誤將導致未預期的錯誤，例如 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中的存取違規。 對於其他的副程式，我們也建議您使用錯誤處理常式。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用 OLE Automation 物件的第一個步驟是呼叫 **sp_OACreate** 系統預存程序，以便在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的位址空間中建立物件的執行個體。  
  
 在建立物件的執行個體之後，請呼叫下列預存程序來使用物件的相關屬性、方法與錯誤資訊：  
  
-   **sp_OAGetProperty** 取得屬性的值。  
  
-   **sp_OASetProperty** 設定屬性的值。  
  
-   **sp_OAMethod** 呼叫一個方法。  
  
-   **sp_OAGetErrorInfo** 取得最近的錯誤資訊。  
  
 當您不再需要物件時，可呼叫 **sp_OADestroy** 來將使用 **sp_OACreate**所建立的物件執行個體取消配置。  
  
 OLE Automation 物件會透過屬性值和方法傳回資料。 **sp_OAGetProperty** 和 **sp_OAMethod** 會以結果集形式傳回這些資料值。  
  
 OLE Automation 物件的範圍是一個批次。 該物件的所有參考都必須包含於一個批次、預存程序或觸發程序內。  
  
 在參考物件時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE Automation 物件支援將參考的物件跨越它所包含的其他物件。 例如，在使用 SQL-DMO **SQLServer** 物件時，您可參考至該伺服器所包含的資料庫與資料表。  
  
## <a name="related-content"></a>相關內容  
 [物件階層語法 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql)  
  
 [介面區組態](../security/surface-area-configuration.md)  
  
 [OLE Automation 程序伺服器組態選項](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oacreate-transact-sql)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oamethod-transact-sql)  
  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oadestroy-transact-sql)  
  
  
