---
title: 資料類型 (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e135e6706454fe1f03b4c7ab762e5234e1b7d35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064211"
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
|SRVFLTN|**real** &#124; **float null**|**real** 或 **float** 資料類型，允許 Null 值。|  
|SRVIMAGE|**image**|**image** 資料類型。|  
|SRVINT1|**tinyint**|1-byte **tinyint** 資料類型。|  
|SRVINT2|**smallint**|2-byte **smallint** 資料類型。|  
|SRVINT4|**int**|4-byte **int** 資料類型。|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|**tinyint**、**smallint** 或 **int** 資料類型，允許 Null 值。|  
|SRVMONEY4|**smallmoney**|4-byte **smallmoney** 資料類型。|  
|SRVMONEY|**money**|8-byte **money** 資料類型。|  
|SRVMONEYN|**money** &#124; **smallmoney null**|**smallmoney** 或 **money** 資料類型，允許 Null 值。|  
|SRVNCHAR|**nchar**|Unicode **character** 資料類型。|  
|SRVNTEXT|**ntext**|Unicode **text** 資料類型。|  
|SRVNUMERIC|**numeric**|**numeric** 資料類型。|  
|SRVNUMERICN|**numeric null**|**numeric** 資料類型，允許 Null 值。|  
|SRVNVARCHAR|**nvarchar**|Unicode 可變長度的 **character** 資料類型。|  
|SRVTEXT|**text**|**text** 資料類型。|  
|SRVVARBINARY|**varbinary**|可變長度的 **binary** 資料類型。|  
|SRVVARCHAR|**varchar**|可變長度的 **character** 資料類型。|  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
