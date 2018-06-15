---
title: 預設 PHP 資料類型 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 432b09a03f9f0d7704ed50de92db64417b624ba8
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307697"
---
# <a name="default-php-data-types"></a>預設 PHP 資料類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

從伺服器擷取資料時，如果使用者尚未指定任何 PHP 資料類型，則 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會將資料轉換成預設 PHP 資料類型。  
  
使用 PDO_SQLSRV 驅動程式傳回資料時，資料類型會是 int 或 string。  
  
本主題的其餘部分將討論使用 SQLSRV 驅動程式的預設資料類型。  
  
下表列出 SQL Server 資料類型 (從伺服器擷取的資料類型)、預設 PHP 資料類型 (資料會轉換成的資料類型)，以及資料流和字串的預設編碼。 如需從伺服器擷取資料時如何指定資料類型的詳細資訊，請參閱 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)。  
  
|SQL Server 類型|預設 PHP 類型|預設編碼|  
|-------------------|--------------------|--------------------|  
|BIGINT|String|8 位元字元<sup>1</sup>|  
|BINARY|資料流<sup>2</sup>|二進位<sup>3</sup>|  
|bit|Integer|8 位元字元<sup>1</sup>|  
|char|String|8 位元字元<sup>1</sup>|  
|date<sup>4</sup>|DATETIME|不適用|  
|datetime<sup>4</sup>|DATETIME|不適用|  
|datetime2<sup>4</sup>|DATETIME|不適用|  
|datetimeoffset<sup>4</sup>|DATETIME|不適用|  
|Decimal|String|8 位元字元<sup>1</sup>|  
|FLOAT|float|8 位元字元<sup>1</sup>|  
|地理位置|資料流|二進位<sup>3</sup>|  
|幾何|資料流|二進位<sup>3</sup>|  
|image<sup>5</sup>|資料流<sup>2</sup>|二進位<sup>3</sup>|  
|ssNoversion|Integer|8 位元字元<sup>1</sup>|  
|money|String|8 位元字元<sup>1</sup>|  
|NCHAR|String|8 位元字元<sup>1</sup>|  
|NUMERIC|String|8 位元字元<sup>1</sup>|  
|NVARCHAR|String|8 位元字元<sup>1</sup>|  
|nvarchar(MAX)|資料流<sup>2</sup>|8 位元字元<sup>1</sup>|  
|ntext<sup>6</sup>|資料流<sup>2</sup>|8 位元字元<sup>1</sup>|  
|REAL|float|8 位元字元<sup>1</sup>|  
|smalldatetime|DATETIME|8 位元字元<sup>1</sup>|  
|SMALLINT|Integer|8 位元字元<sup>1</sup>|  
|SMALLMONEY|String|8 位元字元<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|8 位元字元<sup>1</sup>|  
|文字<sup>8</sup>|資料流<sup>2</sup>|8 位元字元<sup>1</sup>|  
|time<sup>4</sup>|DATETIME|不適用|  
|TIMESTAMP|String|8 位元字元<sup>1</sup>|  
|TINYINT|Integer|8 位元字元<sup>1</sup>|  
|UDT|資料流<sup>2</sup>|二進位<sup>3</sup>|  
|UNIQUEIDENTIFIER|字串<sup>9</sup>|8 位元字元<sup>1</sup>|  
|varbinary|資料流<sup>2</sup>|二進位<sup>3</sup>|  
|varbinary(MAX)|資料流<sup>2</sup>|二進位<sup>3</sup>|  
|varchar|String|8 位元字元<sup>1</sup>|  
|varchar(MAX)|資料流<sup>2</sup>|8 位元字元<sup>1</sup>|
|xml|資料流<sup>2</sup>|8 位元字元<sup>1</sup>|  
  

1.  資料會以如同在系統上設定之 Windows 地區設定的字碼頁中指定的 8 位元字元傳回。 以單一位元組問號 （？） 字元取代任何多位元組字元或未對應到此字碼頁的字元。  
  
2.  如果[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)或[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)是用來擷取預設 PHP 類型的資料流的資料，資料會以字串傳回具有相同的編碼方式與資料流。 例如，如果 SQL Server 二進位類型會擷取使用**sqlsrv_fetch_array**，則預設傳回類型是二進位字串。  
  
3.  資料會以原始位元組資料流形式從伺服器傳回，而不需執行編碼或轉譯。  

4.  可以字串形式擷取日期和時間。 如需詳細資訊，請參閱 [如何：使用 SQLSRV 驅動程式，以字串的形式擷取日期和時間類型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)。  

5.  這是對應至 varbinary(max) 類型的傳統類型。

6. 這是對應至 nvarchar(max) 類型的傳統類型。

7.  雙向或輸出參數中不支援 sql_variant。

8.  這是對應至 varchar(max) 類型的傳統類型。  
  
9.  UNIQUEIDENTIFIER 是下列規則運算式所代表的 GUID：  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>其他新的 SQL Server 2008 資料類型和功能  
中不支援資料類型的新 SQL Server 2008 中，以及存在於外部資料行 （例如資料表值參數） [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。 下表摘要說明 SQL Server 2008 新功能的 PHP 支援。  
  
|功能|PHP 支援|  
|-----------|---------------|  
|資料表值參數|否|  
|疏鬆資料行|Partial|  
|Null 位元壓縮|是|  
|大型 CLR 使用者定義型別 (UDT)|是|  
|服務主體名稱|否|  
|MERGE|是|  
|FILESTREAM|Partial|  
  
部分類型支援表示您無法以程式設計方式查詢資料行的類型。  
  
## <a name="see-also"></a>另請參閱  
[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Converting Data Types](../../connect/php/converting-data-types.md)

[PHP 類型](http://php.net/manual/en/language.types.php)

[資料類型 (TRANSACT-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
