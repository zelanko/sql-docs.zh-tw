---
title: 暫停追蹤
titleSuffix: SQL Server Profiler
description: 了解如何暫停追蹤，讓 SQL Server Profiler 停止擷取事件資料，並查看當追蹤暫停時可變更的屬性。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 9a30e6d06137eddf2f8a9796c69cfe20fb9ab976
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774772"
---
# <a name="pause-a-trace-sql-server-profiler"></a>暫停追蹤 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
暫停追蹤可避免進一步擷取事件資料，直到追蹤重新啟動為止。  
  
 暫停追蹤可防止事件資料被擷取，直到重新啟動追蹤為止。 重新啟動追蹤可讓追蹤作業繼續進行。 重新啟動之後，先前擷取的資料並不會遺失。 當追蹤重新啟動時，資料的擷取動作會從該暫停點繼續進行。 當追蹤暫停時，您可以變更名稱、事件、資料行及篩選條件。 但是，您無法變更傳送追蹤資料的目的地，也不能變更伺服器連接。  
  
### <a name="to-pause-a-trace"></a>若要暫停追蹤  
  
1.  選取包含執行中追蹤的視窗。  
  
2.  在 **[檔案]** 功能表上，按一下 **[暫停追蹤]** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
