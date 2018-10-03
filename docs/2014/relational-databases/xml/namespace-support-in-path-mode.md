---
title: PATH 模式中的命名空間支援 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d0c123a3cf77a04ee42f66ba0faf5bd995714c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219868"
---
# <a name="namespace-support-in-path-mode"></a>PATH 模式中的命名空間支援
  PATH 模式中的命名空間支援是使用 WITH NAMESPACES 來提供。 例如，下列查詢示範 WITH NAMESPACES 語法以宣告命名空間 ("a:")，它可用於後續的 SELECT 陳述式中：  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>範例  
 以下範例說明使用 PATH 模式從 SELECT 查詢產生 XML。 這些查詢中有許多是針對自行車製造指示的 XML 文件所指定，這些文件是儲存在 ProductModel 資料表的 Instructions 資料行中。  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)  
  
  
