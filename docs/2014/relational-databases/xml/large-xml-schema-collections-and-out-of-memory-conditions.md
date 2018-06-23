---
title: 大型的 XML 結構描述集合與記憶體不足的情況 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 73bcf8bf2fd6d4c0e8e92e9d0727ddd76b8a5081
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133379"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>大型的 XML 結構描述集合與記憶體不足的情況
  在大型的 XML 結構描述集合中呼叫內建 XML_SCHEMA_NAMESPACE() 函數時，或是當您嘗試卸除大型 XML 結構描述集合時，就可能會發生記憶體不足的情況。 下列是您可用來處理此情形的解決方案：  
  
-   當系統負載很輕時，使用 DROP_XML_SCHEMA_COLLECTION 命令。 如果這個命令失敗，請使用 ALTER DATABASE 陳述式和再次嘗試 DROP XML SCHEMA COLLECTION，以便將資料庫切換到單一使用者模式中。 如果 XML 結構描述集合存在於 **master**、 **model**或 **tempdb**中，則單一使用者模式將需要重新啟動伺服器。  
  
-   當您呼叫 XML_SCHEMA_NAMESPACE 時，可以嘗試擷取單一 XML 結構描述命名空間、可以在系統負載較輕時嘗試呼叫，也可以在單一使用者模式中嘗試呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  