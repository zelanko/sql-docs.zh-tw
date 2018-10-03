---
title: 無效的具名的管道名稱可能會防止升級 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d800001d2bf5ec663ad2c3651aae59baccca445b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057848"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>無效的具名管道名稱，可能會防止升級
  如果具名管道通訊協定的設定不正確，升級就會失敗。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在升級期間，安裝程式會啟動[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]具有共用的記憶體支援的執行個體，僅接受本機連接是具名的管道。 如果在伺服器上指定的管道名稱不是空白的它必須開始使用字串"\\\\。 \pipe\\」 為有效。 如果管道名稱無效，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就不會啟動，而且安裝會失敗。  
  
## <a name="corrective-action"></a>更正動作  
 使用**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網路公用程式**來提供有效的管道名稱，然後執行安裝程式。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
