---
title: Excel 自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8d556a199b608659a9ceaaeb3b7036155886d6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827231"
---
# <a name="excel-custom-properties"></a>Excel 自訂屬性
  **來源自訂屬性**  
  
 Excel 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 Excel 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用來存取資料庫的模式。 可能的值為**Open Rowset**，**開啟的資料列集，從變數**， `SQL Command`，和**來自變數的 SQL 命令**。 預設值為 **[開啟資料列集]**。|  
|CommandTimeout|Integer|命令逾時之前的秒數。值為 0 表示無限逾時。<br /><br /> **注意**：雖然您無法在 [Excel 來源編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|[OpenRowset]|String|用來開啟資料列集之資料庫物件的名稱。|  
|OpenRowsetVariable|String|變數，其中包含用來開啟資料列集之資料庫物件的名稱。|  
|ParameterMapping|String|從 SQL 命令中的參數到變數的對應。|  
|SqlCommand|String|要執行的 SQL 命令。|  
|SqlCommandVariable|String|變數，其中包含要執行的 SQL 命令。|  
  
 Excel 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Excel 來源](excel-source.md)。  
  
 **目的地自訂屬性**  
  
 Excel 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 Excel 目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定目的地如何存取其目的地資料庫。<br /><br /> 此屬性可以有下列其中一個值：<br /><br /> `OpenRowset` (0)-您提供的資料表或檢視表名稱。<br /><br /> `OpenRowset from Variable` (1)-您可以提供包含資料表或檢視名稱變數的名稱。<br /><br /> `OpenRowset Using Fastload` (3)-您提供的資料表或檢視表名稱。<br /><br /> `OpenRowset Using Fastload from Variable` (4)-您可以提供包含資料表或檢視名稱變數的名稱。<br /><br /> `SQL Command` (2)-您提供的 SQL 陳述式。|  
|CommandTimeout|Integer|逾時之前 SQL 命令可以執行的秒數上限。值為 **0** 指出無限的時間。 這個屬性的預設值為 **0**。<br /><br /> 注意:雖然您無法在 [Excel 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|FastLoadKeepIdentity|布林|一個值，指定載入資料時是否要複製識別值。 只有在您使用其中一個快速載入選項時，才能使用這個屬性。 此屬性的預設值為 **False**。|  
|FastLoadKeepNulls|布林|一個值，指定載入資料時是否要複製 Null 值。 這個屬性只能搭配其中一個快速載入選項使用。 此屬性的預設值為 **False**。|  
|FastLoadMaxInsertCommitSize|Integer|一個值，指定快速載入作業期間，Excel 目的地嘗試認可的批次大小。 預設值為 **2147483647**。 **0** 的值表示處理所有資料列之後的單一認可作業。|  
|FastLoadOptions|String|快速載入選項的集合。 快速載入選項包括資料表的鎖定和條件約束的檢查。 您可以指定其中一個選項、兩個選項或不指定任何選項。<br /><br /> 注意:雖然您無法在 [Excel 目的地編輯器] 中使用這個屬性的某些選項，但是可以使用 [進階編輯器] 來設定這些選項。|  
|OpenRowset|String|當 AccessMode 為`OpenRowset`，資料表或檢視 Excel 目的地所存取的名稱。|  
|OpenRowsetVariable|String|當 AccessMode 為`OpenRowset from Variable`，包含名稱的資料表或檢視 Excel 目的地所存取的變數名稱。|  
|SqlCommand|String|當 AccessMode 為`SQL Command`，是 Excel 目的地用來指定資料的目的地資料行的 TRANSACT-SQL 陳述式。|  
  
 Excel 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Excel 目的地](excel-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
