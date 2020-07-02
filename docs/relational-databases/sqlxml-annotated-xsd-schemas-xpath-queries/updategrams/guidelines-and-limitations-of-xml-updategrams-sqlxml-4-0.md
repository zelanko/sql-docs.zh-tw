---
title: Updategram 的指導方針和限制（SQLXML）
description: 瞭解在 SQLXML 4.0 中使用 XML updategram 的指導方針和限制。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb774fd8dbb05b52e4f57fcf78d4ecd4c923ccb8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790650"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指導方針和限制 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  使用 XML Updategram 時，請記住下列事項：  
  
-   如果您針對僅具有一組和區塊的插入作業使用 updategram **\<before>** **\<after>** ，則 **\<before>** 可以省略區塊。 相反地，在刪除作業時， **\<after>** 可以省略區塊。  
  
-   如果您在標記中使用具有多個 **\<before>** 和區塊的 updategram，則 **\<after>** **\<sync>** **\<before>** 必須同時 **\<after>** 指定區塊和區塊來形成 **\<before>** 和 **\<after>** 配對。  
  
-   Updategram 中的更新會套用到 XML 結構描述所提供的 XML 檢視。 因此，若要讓預設的對應成功，您必須在 Updategram 中指定結構描述檔案名稱，或者，如果沒有提供檔案名稱，元素和屬性名稱必須符合資料庫中的資料表和資料行名稱。  
  
-   SQLXML 4.0 要求 Updategram 中的所有資料行值都必須在提供的結構描述 (XDR 或 XSD) 中明確對應，才能構成其子元素的 XML 檢視。 這個行為與舊版的 SQLXML 不同，如果在**sql： relationship**注釋中隱含為外鍵的一部分，則允許在架構中未對應的資料行值。 (請注意，此變更不會影響主索引鍵值傳播到子元素，如果沒有針對子元素明確指定任何值，仍然會發生在 SQLXML 4.0 上。  
  
-   如果您使用 updategram 來修改二進位資料行中的資料（例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **image**資料類型），您必須提供對應架構，其中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 必須指定資料類型（例如， **sql： datatype = "image"**）和 XML 資料類型（例如**dt： type = "binhex"** 或**dt： type = "binbase64**）。 您必須在 updategram 中指定 binary 資料行的資料。updategram 會忽略對應架構中指定的**sql： url 編碼**注釋。  
  
-   當您撰寫 XSD 架構時，如果您為 [ **sql：關聯**] 或 [ **sql：] 欄位**注釋指定的值包含特殊字元，例如空白字元（例如，在 "order details" 資料表名稱中），這個值必須以方括弧括住（例如，"[order details]"）。  
  
-   使用 Updategram 時，不支援鏈結關聯性。 例如，如果資料表 A 和 C 透過使用資料表 B 的鏈結關聯性相關聯，嘗試執行 Updategram 時，會發生下列錯誤：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使結構描述和 Updategram 都正確而且格式有效，如果存在鏈結關聯性，則會發生此錯誤。  
  
-   Updategram 不允許在更新期間傳遞**映射**類型資料做為參數。  
  
-   使用 updategram 時，不應該在中的區塊中使用像**text/Ntext**和 images 之類的二進位大型物件（BLOB）類型 **\<before>** ，因為這會包含它們以在並行控制中使用。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中會使用 LIKE 關鍵字來比較**text**資料類型的資料行;不過，如果 BLOB 類型的資料大小大於8K，比較將會失敗。  
  
-   **Ntext**資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，在 updategram 的區塊中使用 "[Serializable]" **\<before>** 時，在**Ntext**類型的資料行並行檢查中使用時，將會失敗，並出現下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
