---
title: 以 IOpenRowset 建立資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30ba5a4d1cbe326be567a3be18cd7a76371f7e49
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417937"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>以 IOpenRowset 建立資料列集
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會支援**iopenrowset:: Openrowset**方法具有下列限制：  
  
-   基底資料表或檢視表中必須指定資料庫識別碼 (DBID) 結構*Createtable*參數所指向。  
  
-   DBID *eKind*成員必須指示 DBKIND_NAME。  
  
-   DBID *uName*成員必須指定現有的基底資料表或檢視表的名稱為 Unicode 字元字串。  
  
-   *PIndexID*的參數**OpenRowset**必須是 NULL。  
  
 結果集會**iopenrowset:: Openrowset**包含單一資料列集。 包含單一資料列集結果集可受到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料指標。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](rowsets.md)  
  
  
