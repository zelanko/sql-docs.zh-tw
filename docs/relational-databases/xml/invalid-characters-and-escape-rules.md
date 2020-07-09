---
title: 無效的字元和逸出規則 | Microsoft Docs
description: 了解 FOR XML 子句如何處理無效的 XML 字元，並了解 XML 名稱中無效字元的逸出規則。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 592aa9b31ce957500210a9a4d3caa7f780bf588d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738429"
---
# <a name="invalid-characters-and-escape-rules"></a>無效的字元和逸出規則
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  此主題描述 FOR XML 子句如何處理無效的 XML 字元，並列出 XML 名稱中無效字元的逸出規則。  
  
## <a name="for-xml-and-invalid-characters"></a>XML 和無效的字元  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在不使用 TYPE 指示詞的 FOR XML 查詢中傳回無效的 XML 字元時，會將這些字元實體化。  
  
 雖然不論這些字元是否已實體化，XML 1.0 相容剖析器都會引發剖析錯誤，但實體化格式與 XML 1.1 之間的相容性已有所提升。 實體化格式與未來的 XML 標準版本之間也將具有較好的相容性。 此外，它還可簡化偵錯作業，因為已可看見無效字元的字碼指標。  
  
 對於 XML 工具的使用者，則不需使用任何解決方案，因為無論如何 XML 剖析器都會在資料流中出現無效字元時失敗。 若您使用非 XML 工具，則此項變更需要您更新程式設計邏輯，使其搜尋這些當做實體化值的字元。  
  
 目前已可透過不同的方式在 FOR XML 查詢中實體化下列空白字元，以便在往返過程中保留這些字元：  
  
-   在元素內容和屬性中： **hex(0D)** (歸位字元)  
  
-   在屬性內容中： **hex(09)** (定位字元)、 **hex(0A)** (換行字元)  
  
 輸出中會保留這些字元，且剖析器不會將其正規化。  
  
## <a name="escape-rules"></a>逸出規則  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 若名稱中含有對 XML 名稱而言無效的字元 (如空格)，則會在轉譯為 XML 名稱時，將該無效字元轉譯為逸出的數值實體編碼。  
  
 XML 名稱中只允許兩種非字母字元：冒號 (:) 和底線 (_)。 這是因為冒號已保留給命名空間，而底線已被選為逸出字元。 以下是適用於編碼的逸出規則：  
  
-   根據 XML 1.0 規格，任何不屬於有效 XML 名稱字元的 UCS-2 字元，都會逸出為 _xHHHH\_。 HHHH 代表最高階位元優先順序之字元的四位數十六進位 UCS-2 碼。 例如，資料表名稱 **Order Details** 會編碼為 Order_x0020_Details。  
  
-   不符合 UCS-2 範圍 (UCS-4 新增的，範圍介於 U+00010000 與 U+0010FFFF 之間) 的字元都會編碼為 _xHHHHHHHH\_。 在 SQL Server 2000 回溯相容性模式中，HHHHHHHH 代表字元的八位數十六進位 UCS-4 編碼。 在其他情況下，字元會編碼為 _xHHHHHH\_，以符合 ISO 標準。  
  
-   除非下一個字元是 x，否則底線字元不需要逸出。 例如，資料表名稱 **Order_Details** 就未編碼。  
  
-   識別碼的冒號也不會逸出，因此命名空間元素及屬性名稱才能夠由 FOR XML 查詢產生。 例如，下列查詢所產生的命名空間屬性在名稱中就有冒號：  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     此查詢產生以下結果：  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     請注意，建議使用 WITH XMLNAMESPACES 來加入 XML 命名空間。  
  
## <a name="see-also"></a>另請參閱  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
