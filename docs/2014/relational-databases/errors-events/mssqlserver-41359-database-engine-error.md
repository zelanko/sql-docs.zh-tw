---
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ecf42a161af2dba5c0444b92fea5a55144b0c7b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089492"
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41359|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|訊息文字|當資料庫選項 READ_COMMITTED_SNAPSHOT 設為 ON 時，使用 READ COMMITTED 隔離等級來存取記憶體最佳化資料表的查詢無法存取磁碟基礎的資料表。 為使用資料表提示例如 WITH (SNAPSHOT) 的記憶體最佳化資料表，提供支援的隔離等級。|  
  
## <a name="explanation"></a>說明  
 READ_COMMITTED_SNAPSHOT=ON 的資料庫不支援存取記憶體最佳化資料表和磁碟基礎之資料表的交易。  
  
## <a name="user-action"></a>使用者動作  
 針對使用資料表層級提示 (例如 WITH (SNAPSHOT)) 的記憶體最佳化資料表，將 READ_COMMITTED_SNAPSHOT 設為 OFF 或提供支援的隔離等級。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
