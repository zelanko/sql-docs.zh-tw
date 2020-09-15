---
description: 使用 SQLSRV 驅動程式以資料流形式擷取資料
title: 使用 SQLSRV 驅動程式以資料流形式擷取資料 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cceb378b0571ff1fb6b3505abd1f6d8f4535a5cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414444"
---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>使用 SQLSRV 驅動程式以資料流形式擷取資料
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以資料流形式擷取資料僅適用於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 SQLSRV 驅動程式，而不適用於 PDO_SQLSRV 驅動程式。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會利用資料流擷取大量的資料。 本節中的主題將詳細說明如何以資料流的形式擷取資料。  
  
下列步驟概述如何以資料流的形式擷取資料：  
  
1.  準備及執行使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或結合了 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 的 Transact-SQL 查詢。  
  
2.  使用 [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 移至結果集內的下一個資料列。  
  
3.  使用 [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 擷取資料列中的欄位。 使用 **SQLSRV_PHPTYPE_STREAM(<encoding>)** 作為函式呼叫中的第三個參數，指定要以資料流的形式擷取資料。 下表列出用來指定編碼及其描述的常數：  
  
    |SQLSRV 常數|描述|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|資料會以原始位元組資料流形式從伺服器傳回，而不需執行編碼或轉譯。|  
    |SQLSRV_ENC_CHAR|資料會以如同在系統上設定之 Windows 地區設定的字碼頁中指定的 8 位元字元傳回。 系統會以單一位元組問號 (?) 字元取代任何多位元組字元或未對應到此字碼頁的字元。|  
  
> [!NOTE]  
> 某些資料類型會依預設以資料流的形式傳回。 如需詳細資訊，請參閱 [Default PHP Data Types](../../connect/php/default-php-data-types.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|---------|---------------|  
|[使用 SQLSRV 驅動程式支援資料流的資料類型](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|列出可以資料流的形式擷取的 SQL Server 資料類型。|  
|[如何：使用 SQLSRV 驅動程式以資料流的形式擷取字元資料](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|示範如何以資料流的形式擷取字元資料。|  
|[如何：使用 SQLSRV 驅動程式以資料流形式擷取二進位資料](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|示範如何以資料流的形式擷取二進位資料。|  
  
## <a name="see-also"></a>另請參閱  
[擷取資料](../../connect/php/retrieving-data.md)

[常數 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
