---
description: 傳輸八位元長度
title: 傳輸八位長度 |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c89a9cb1423693e7d92114233f967d6fb5dcee1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386344"
---
# <a name="transfer-octet-length"></a>傳輸八位元長度
資料行的傳輸八位長度是將資料傳輸到其預設 C 資料類型時，傳回給應用程式的最大位元組數目。 若為字元資料，則傳輸八位長度不包含 null 終止字元的空間。 資料行的傳輸八位長度可能與在資料來源上儲存資料所需的位元組數目不同。  
  
 下表顯示為每個 ODBC SQL 資料類型定義的傳輸八位長度。  
  
|SQL 類型識別碼|長度|  
|-------------------------|------------|  
|所有字元類型 [a]|以位元組為單位之變數類型) 長度的已定義或最大 (。 這與描述項欄位 SQL_DESC_OCTET_LENGTH 的值相同。|  
|SQL_DECIMAL<br />SQL_NUMERIC|如果字元集為 ANSI，則保留此資料的字元表示所需的位元組數目，如果字元集是 UNICODE，則為這個數位的兩倍。 這是數位的數目上限加上二，因為資料是以字元字串的形式傳回，而數位、正負號和小數點則需要字元。 例如，定義為數值 (10，3) 的資料行傳輸長度為12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二進位類型 [a]|針對固定類型保留已定義之 (所需的位元組數目) 或變數類型的最大 () 的字元數。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (SQL_DATE_STRUCT 或 SQL_TIME_STRUCT 結構) 的大小。|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT 結構) 的大小。|  
|所有間隔資料類型|34 (間隔結構) 的大小。|  
|SQL_GUID|16 (GUID 結構) 的大小。|  
| &nbsp; | &nbsp; |

 [a] 如果驅動程式無法判斷變數類型的資料行或參數長度，則會傳回 SQL_NO_TOTAL。
