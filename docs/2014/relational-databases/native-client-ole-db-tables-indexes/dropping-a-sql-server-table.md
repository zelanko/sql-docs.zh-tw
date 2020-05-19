---
title: 卸除 SQL Server 資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6f005b9ab1c3d334242b2a20d47f6e4646d6cef8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704540"
---
# <a name="dropping-a-sql-server-table"></a>卸除 SQL Server 資料表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會公開**ITableDefinition：:D roptable**函數。 這可讓取用者 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從資料庫中移除資料表。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](tables-and-indexes.md)  
  
  
