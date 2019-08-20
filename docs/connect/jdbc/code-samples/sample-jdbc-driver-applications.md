---
title: 範例 JDBC 驅動程式應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ef5c2d71d398be52ebed2b69020e87d54818176
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028309"
---
# <a name="sample-jdbc-driver-applications"></a>範例 JDBC 驅動程式應用程式

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 範例應用程式會示範 JDBC 驅動程式的各種功能。 此外，它們也示範當搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫使用 JDBC 驅動程式時，您可以遵循的良好程式設計作法。  
  
所有的範例應用程式都包含在可以在本機電腦上編譯並執行的 *.java 程式碼檔案中，而且它們位於下列位置的各個子資料夾中：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

 本節的主題說明如何設定並執行範例應用程式，並包括範例應用程式示範內容的討論。  
  
## <a name="in-this-section"></a>本節內容  
  
| 主題                                                                                                                  | 描述                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [連線及擷取資料](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)                              | 這些範例應用程式示範如何連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫。 它們也示範從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫擷取資料的不同方法。 |
| [使用資料類型 &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)                        | 這些範例應用程式示範如何使用 JDBC 驅動程式資料類型方法，來使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中的資料。                                                                                              |
| [使用結果集](../../../connect/jdbc/code-samples/working-with-result-sets.md)                                          | 這些範例應用程式示範如何使用結果集，來處理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中包含的資料。                                                                                                            |
| [使用大型資料](../../../connect/jdbc/code-samples/working-with-large-data.md)                                            | 這些範例應用程式會示範如何使用自適性緩衝來擷取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中的大數值資料，而沒有伺服器資料指標的負擔。                                                         |
| [SQL 資料探索與分類](../../jdbc/code-samples/data-discovery-and-classification-sample.md) | 這個範例應用程式會示範如何使用 JDBC 驅動程式, 從 ResultSet 物件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中, 抓取資料庫中所包含的資料探索和分類資訊。                                            |
  
## <a name="see-also"></a>另請參閱

[JDBC 驅動程式概觀](../../../connect/jdbc/overview-of-the-jdbc-driver.md)
