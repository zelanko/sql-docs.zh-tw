---
title: 在90或更新版本的相容性模式中，CREATE STATISTICS 語句中不支援 WITH ROWS |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090965"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>在 90 或之後的相容性模式中，CREATE STATISTICS 陳述式中不支援 WITH ROWS
  當您執行相容性模式設定為 90 或之後的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，系統不支援在 CREATE STATISTICS 陳述式中指定 WITH ROWS。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 藉由使用範例*數目*資料列來指定，或指定符合記載語法的其他選項，以修改包含資料列的 CREATE STATISTICS 語句。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜CREATE STATISTICS (Transact-SQL)＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
