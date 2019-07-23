---
title: 資料指標類型 (PDO_SQLSRV 驅動程式) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c62c2a35123e77f5366dd5348fd51b3c50c85605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993695"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>資料指標類型 (PDO_SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 驅動程式讓您能夠建立可捲動的結果集，並含有數個資料指標的其中一個。

如需如何使用 PDO_SQLSRV 驅動程式指定資料指標的相關資訊及程式碼範例，請參閱 [PDO::prepare](../../connect/php/pdo-prepare.md)。

## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 和伺服器端資料指標
在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版之前，PDO_SQLSRV 驅動程式讓您能夠建立一個結果集，並含有伺服器端的順向或靜態資料指標。 從 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版開始，也會提供索引鍵集和動態資料指標。

您可以使用 [PDO::prepare](../../connect/php/pdo-prepare.md) 來選取下列其中一個資料指標類型，藉以指定伺服器端資料指標的類型：

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

您可以指定 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`，然後將適當的值傳遞到 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`，藉以要求動態、靜態或索引鍵集資料指標。 您可針對伺服端資料指標傳遞給 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 的可能值如下：

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 和用戶端資料指標
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版中新增用戶端資料指標，讓您能夠在記憶體中快取整個結果集。 其中一個優點是執行查詢之後，就能使用資料列計數。

用戶端資料指標應該用於小型到中型的結果集。 大型結果集應該使用伺服器端資料指標。

在使用用戶端資料指標時，如果緩衝區因為不夠大而無法保存整個結果集，則查詢將傳回 false。 您可以將緩衝區大小上限提高到 PHP 記憶體限制。

您可以設定緩衝區的大小，使用 [PDO::setAttribute](../../connect/php/pdo-setattribute.md) 或 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 的 `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` 屬性來保留結果集。 您也可以在 php.ini 檔案中使用 pdo_sqlsrv.client_buffer_max_kb_size 來設定緩衝區大小上限 (例如 pdo_sqlsrv.client_buffer_max_kb_size = 1024)。

您可以使用 [PDO::prepare](../../connect/php/pdo-prepare.md)、指定 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 資料指標類型，然後指定 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`，來要求用戶端資料指標。

## <a name="example"></a>範例
下列範例說明如何指定已緩衝處理的資料指標。
```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));
$stmt->execute();
print $stmt->rowCount();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

## <a name="see-also"></a>另請參閱
[指定資料指標類型及選取資料列](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)

