---
title: 資料指標類型 （PDO_SQLSRV 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 621bfe1f20b9ca656bf442377b1f453503b86a8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833466"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>資料指標類型 (PDO_SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 驅動程式可讓您建立數個資料指標的其中一個可捲動的結果集。  
  
如需如何指定資料指標使用 PDO_SQLSRV 驅動程式，以及程式碼範例，請參閱[pdo:: prepare](../../connect/php/pdo-prepare.md)。  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 和伺服器端資料指標  
在 3.0 版之前[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，PDO_SQLSRV 驅動程式可讓您建立含有伺服器端順向或靜態資料指標的結果集。 從 3.0 版開始[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，也有 keyset 和 dynamic 資料指標。  
  
您可以使用 pdo:: prepare 或 pdostatement:: Setattribute 來選取其中一種資料指標類型，表示伺服器端資料指標的類型：  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_SCROLL  
  
要求 keyset 或 dynamic 資料指標，您可以指定 pdo:: ATTR_CURSOR = > pdo:: CURSOR_SCROLL，然後再傳遞適當的值，以 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE。 您可以將它傳遞至 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE 的可能值如下：  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 和用戶端資料指標  
在 3.0 版中新增用戶端資料指標[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，可讓您快取的整個結果集在記憶體中。 其中一個優點是之後執行的查詢，就可以使用資料列計數。  
  
用戶端資料指標應該用於小型到中型-大小的結果集。 大型結果集應該使用伺服器端資料指標。  
  
查詢會傳回 false，如果緩衝區不夠大，無法保存的整個結果集時使用的用戶端資料指標。 您可以增加到 PHP 記憶體限制的緩衝區大小。  
  
您可以設定的保留結果的 PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE 屬性集的緩衝區大小[pdo:: setattribute](../../connect/php/pdo-setattribute.md)或是[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)。 您也可以設定的最大的緩衝區大小 pdo_sqlsrv.client_buffer_max_kb_size php.ini 檔案中 (例如 pdo_sqlsrv.client_buffer_max_kb_size = 1024年)。  
  
您表示您使用 pdo:: prepare 或 pdostatement:: Setattribute 想用戶端資料指標，並選取 pdo:: ATTR_CURSOR = > pdo:: CURSOR_SCROLL 資料指標類型。  接著您可以指定 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE = > PDO::SQLSRV_CURSOR_BUFFERED。  
  
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
  
