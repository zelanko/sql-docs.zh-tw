---
title: MSSQLSERVER_17066 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17066 (Database Engine error)
ms.assetid: 7d650bbf-c583-4af8-9e22-993ee2880d95
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cf83c11229024b7214b7fca7d777b3d2b46d2b06
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68100393"
---
# <a name="mssqlserver_17066"></a>MSSQLSERVER_17066
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17066|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLASSERT_ONLY|  
|訊息文字|SQL Server 判斷提示: 檔案: \<%s>，行 = %d 失敗的判斷提示 = '%s'。 此錯誤可能與時間有關。 如果重新執行陳述式之後仍然發生此錯誤，請使用 DBCC CHECKDB 來檢查資料庫的結構完整性，或重新啟動伺服器以確定記憶體中的資料結構並未損毀。|  
  
## <a name="explanation"></a>說明  
這項錯誤可能是由暫時性的時間相關錯誤所造成，或由記憶體中或磁碟內存的資料損毀所造成。  
  
## <a name="user-action"></a>使用者動作  
請重新執行導致引發此例外狀況的陳述式。 如果此錯誤是由時間相關的事件所造成，此錯誤可能不會再次發生。 如果持續發生此問題，請執行 DBCC CHECKDB 來檢查是否有磁碟內存的損毀。 重新啟動伺服器，以便確保記憶體中的資料結構並未損毀。  
  
## <a name="see-also"></a>另請參閱  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
