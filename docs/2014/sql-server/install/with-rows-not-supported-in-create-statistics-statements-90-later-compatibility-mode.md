---
title: 在 90 或之後的相容性模式中的 CREATE STATISTICS 陳述式不會支援 WITH ROWS |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9d509352d99cab9359e7ea222f5fb2d5d7e28075
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131622"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>在 90 或之後的相容性模式中，CREATE STATISTICS 陳述式中不支援 WITH ROWS
  當您執行相容性模式設定為 90 或之後的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，系統不支援在 CREATE STATISTICS 陳述式中指定 WITH ROWS。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 藉由指定 WITH SAMPLE 包含 WITH ROWS 的 CREATE STATISTICS 陳述式修改*數目*資料列，或指定其他選項符合所記載語法。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜CREATE STATISTICS (Transact-SQL)＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
