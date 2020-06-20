---
title: 不正確具名管道名稱可能會封鎖升級 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: bacfd3d097d7cccb0a5780328c4db95dc5afc733
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059246"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>無效的具名管道名稱，可能會防止升級
  如果具名管道通訊協定的設定不正確，升級就會失敗。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在升級期間，安裝程式會啟動 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 具有共用記憶體支援的實例，這是僅接受本機連接的具名管道。 如果伺服器上指定的管道名稱不是空白，它必須以字串 "成 .\pipe" 開頭，才 \\ \\ \\ 會是有效的。 如果管道名稱無效，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就不會啟動，而且安裝會失敗。  
  
## <a name="corrective-action"></a>更正動作  
 使用** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路公用程式**來提供有效的管道名稱，然後執行安裝程式。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
