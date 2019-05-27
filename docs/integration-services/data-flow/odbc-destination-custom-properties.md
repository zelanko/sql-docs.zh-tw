---
title: ODBC 目的地自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9c1775b42624d755da4642d0c17c277c3b254eb4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726664"
---
# <a name="odbc-destination-custom-properties"></a>ODBC Destination Custom Properties

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  下表描述 ODBC 目的地的自訂屬性。 所有屬性都可從 SSIS 屬性運算式設定。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|連接|ODBC 連接|用來存取目的地資料庫的 ODBC 連接。|  
|BatchSize|Integer|大量載入的批次大小。 這是當做批次載入的資料列數目。 這只適用於支援資料列取向的參數繫結時。 如果不支援資料列取向的參數繫結，則批次大小為 1。|  
|BindCharColumnAs|整數 (列舉)|此屬性決定 ODBC 目的地如何繫結具有多位元組字串類型 (如 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR) 的資料行。<br /><br /> 可能值為 Unicode (0) 和 ANSI (1)。前者繫結 SQL_C_WCHAR 等資料行，後者則繫結 SQL_C_CHAR 等資料行。 預設值為 Unicode (0)。<br /><br /> 對於支援繫結 CHAR 參數做為寬字元字串的大多數 ODBC 3.x 提供者和 ODBC 2.x 提供者，Unicode 是最佳選項。 當您選取 Unicode 而且 ExposeCharColumnsAsUnicode 為 True 時，使用者不需要指定來源資料庫所用的字碼頁。<br /><br /> **注意：** 雖然您無法在 [ODBC 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|BindNumericAs|整數 (列舉)|此屬性決定 ODBC 目的地如何繫結具有 SQL_TYPE_NUMERIC 和 SQL_TYPE_DECIMAL 資料類型之數值資料的資料行。<br /><br /> 可能值為 Char (0) 和 Numeric (1)。前者繫結 SQL_C_CHAR 等資料行，後者則繫結 SQL_C_NUMERIC 等資料行。 預設值為 Char (0)。<br /><br /> **注意**：雖然您無法在 [ODBC 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|DefaultCodePage|Integer|要用於字串資料行的字碼頁。<br /><br /> **注意**：雖然您無法在 [ODBC 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|InsertMethod|整數 (列舉)|用於插入資料的方法。 可能值為逐列 (0) 和批次 (1)。 預設值為批次 (1)。<br /><br /> 如需這些選項的詳細資訊，請參閱 [ODBC 目的地](../../integration-services/data-flow/odbc-destination.md)中的＜載入選項＞。|  
|StatementTimeout|Integer|在傳回至應用程式並出現錯誤之前等候 SQL 陳述式執行的秒數。 預設值為 120。|  
|TableName|String|要插入資料的目的地資料表名稱。|  
|TransactionSize|Integer|單一交易中的插入數目。 預設值為 0，表示 ODBC 目的地以自動認可模式運作。<br /><br /> 因為 ODBC 連接管理員不支援分散式交易，所以可將此屬性設為 0 以外的值。 不過，如果連接管理員的 **RetainSameConnection** 屬性設為 **true** ，此屬性必須設為 0。<br /><br /> **注意**：雖然您無法在 [ODBC 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|LobChunkSize|Integer|LOB 資料行的區塊大小配置。|  
  
  
