---
title: 產生多個資料列集結果的命令 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d78b0144e112ca868f990ab87d5c58a798b0c55
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056423"
---
# <a name="commands-generating-multiple-rowset-results"></a>產生多個資料列集結果的命令
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者可以從語句傳回多個資料列集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式在下列條件下會傳回多個資料列集結果：  
  
-   批次的 SQL 陳述式以單一命令提交。  
  
-   預存程序實作 SQL 陳述式批次。  
  
## <a name="batches"></a>批次  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會將分號字元辨識為 SQL 語句的批次分隔符號：  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 以一個批次傳送多個 SQL 陳述式，比分開執行每個 SQL 陳述式的效率高。 傳送單一批次可以減少從用戶端到伺服器的網路往返數。  
  
## <a name="stored-procedures"></a>預存程序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對預存程序中的每個陳述式傳回結果集，所以大部分的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回多個結果集。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IMultipleResults 來處理多個結果集](using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令](commands.md)  
  
  
