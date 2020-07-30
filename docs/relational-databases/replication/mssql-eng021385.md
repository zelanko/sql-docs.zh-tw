---
title: MSSQL_ENG021385 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 491c7b44aaa9bfb8a732e0f95aecb4fea4086386
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363296"
---
# <a name="mssql_eng021385"></a>MSSQL_ENG021385
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21385|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|快照集無法處理發行集 '%s'。 可能是由於有使用中的結構描述變更活動，或是正在加入新的發行項。|  
  
## <a name="explanation"></a>說明  
 如果尚有對發行集資料庫的變更在進行 (包括新增或卸除發行項，以及在已發行物件上執行結構描述變更)，而此時便開始執行「快照集代理程式」，即會引發此錯誤。  
  
## <a name="user-action"></a>使用者動作  
 在對發行集資料庫的變更完成後，重新啟動「快照集代理程式」。 如需詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
