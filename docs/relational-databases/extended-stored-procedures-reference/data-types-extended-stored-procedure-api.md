---
title: "資料類型 (擴充預存程序 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a69f167e3979a975deb506270843886142244dc4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="data-types-extended-stored-procedure-api"></a>資料類型 (擴充預存程序 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 若要使用擴充預存程序 API 資料類型，請在程式中包含 Srv.h 標頭檔案。  
  
|資料類型|SQL Server 資料類型|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|**binary** 資料類型，長度為 0 到 8000 個位元組。|  
|SRVBIGCHAR|**char**|**character** 資料類型，長度為 0 到 8000 個位元組。|  
|SRVBIGVARBINARY|**varbinary**|可變長度的 **binary** 資料類型，長度為 0 到 8000 個位元組。|  
|SRVBIGVARCHAR|**varchar**|可變長度的 **character** 資料類型，長度為 0 到 8000 個位元組。|  
|SRVBINARY|**binary**|**binary** 資料類型。|  
|SRVBIT|**Bit**|**bit** 資料類型。|  
|SRVBITN|**bit null**|**bit** 資料類型，允許 Null 值。|  
|SRVCHAR|**char**|**character** 資料類型。|  
|SRVDATETIME|**datetime**|8-byte **datetime** 資料類型。|  
|SRVDATETIM4|**smalldatetime**|4-byte **smalldatetime** 資料類型。|  
|SRVDATETIMN|**datetime null**|**smalldatetime** 或 **datetime** 資料類型，允許 Null 值。|  
|SRVDECIMAL|**decimal**|**decimal** 資料類型。|  
|SRVDECIMALN|**decimal null**|**decimal** 資料類型，允許 Null 值。|  
|SRVFLT4|**real**|4-byte **real** 資料類型。|  
|SRVFLT8|**float**|8-byte **float** 資料類型。|  
|SRVFLTN|**real** &#124;**浮動 null**|**real** 或 **float** 資料類型，允許 Null 值。|  
|SRVIMAGE|**image**|**image** 資料類型。|  
|SRVINT1|**tinyint**|1-byte **tinyint** 資料類型。|  
|SRVINT2|**smallint**|2-byte **smallint** 資料類型。|  
|SRVINT4|**int**|4-byte **int** 資料類型。|  
|SRVINTN|**tinyint** &#124;**smallint** &#124;**int null**|**tinyint**、**smallint** 或 **int** 資料類型，允許 Null 值。|  
|SRVMONEY4|**smallmoney**|4-byte **smallmoney** 資料類型。|  
|SRVMONEY|**money**|8-byte **money** 資料類型。|  
|SRVMONEYN|**money** &#124;**smallmoney null**|**smallmoney** 或 **money** 資料類型，允許 Null 值。|  
|SRVNCHAR|**nchar**|Unicode **character** 資料類型。|  
|SRVNTEXT|**ntext**|Unicode **text** 資料類型。|  
|SRVNUMERIC|**numeric**|**numeric** 資料類型。|  
|SRVNUMERICN|**numeric null**|**numeric** 資料類型，允許 Null 值。|  
|SRVNVARCHAR|**nvarchar**|Unicode 可變長度的 **character** 資料類型。|  
|SRVTEXT|**text**|**text** 資料類型。|  
|SRVVARBINARY|**varbinary**|可變長度的 **binary** 資料類型。|  
|SRVVARCHAR|**varchar**|可變長度的 **character** 資料類型。|  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
