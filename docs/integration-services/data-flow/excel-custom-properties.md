---
title: Excel 自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5217d0b8e3bd9e786e8afa18b2561f5e154ca938
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639315"
---
# <a name="excel-custom-properties"></a>Excel 自訂屬性
  **來源自訂屬性**  
  
 Excel 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 Excel 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用來存取資料庫的模式。 可能的值包括 **[開啟資料列集]**、 **[來自變數的開啟資料列集]**、 **[SQL 命令]** 和 **[來自變數的 SQL 命令]**。 預設值為 **[開啟資料列集]**。|  
|CommandTimeout|Integer|命令逾時之前的秒數。值為 0 表示無限逾時。<br /><br /> **注意**：雖然您無法在 [Excel 來源編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|[OpenRowset]|String|用來開啟資料列集之資料庫物件的名稱。|  
|OpenRowsetVariable|String|變數，其中包含用來開啟資料列集之資料庫物件的名稱。|  
|ParameterMapping|String|從 SQL 命令中的參數到變數的對應。|  
|SqlCommand|String|要執行的 SQL 命令。|  
|SqlCommandVariable|String|變數，其中包含要執行的 SQL 命令。|  
  
 Excel 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Excel 來源](../../integration-services/data-flow/excel-source.md)。  
  
 **目的地自訂屬性**  
  
 Excel 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 Excel 目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定目的地如何存取其目的地資料庫。<br /><br /> 此屬性可以有下列其中一個值：<br /><br /> **OpenRowset** (0) - 您必須提供資料表或檢視表的名稱。<br /><br /> **從變數 OpenRowset** (1) - 您必須提供包含資料表或檢視表名稱之變數的名稱。<br /><br /> **使用 FastLoad OpenRowset** (3) - 您必須提供資料表或檢視表的名稱。<br /><br /> **從變數使用 FastLoad OpenRowset** (4) - 您必須提供包含資料表或檢視表名稱之變數的名稱。<br /><br /> **SQL 命令** (2) - 您要提供 SQL 陳述式。|  
|CommandTimeout|Integer|逾時之前 SQL 命令可以執行的秒數上限。值為 **0** 指出無限的時間。 這個屬性的預設值為 **0**。<br /><br /> 注意：雖然您無法在 [Excel 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|FastLoadKeepIdentity|布林|一個值，指定載入資料時是否要複製識別值。 只有在您使用其中一個快速載入選項時，才能使用這個屬性。 此屬性的預設值為 **False**。|  
|FastLoadKeepNulls|布林|一個值，指定載入資料時是否要複製 Null 值。 這個屬性只能搭配其中一個快速載入選項使用。 此屬性的預設值為 **False**。|  
|FastLoadMaxInsertCommitSize|Integer|一個值，指定快速載入作業期間，Excel 目的地嘗試認可的批次大小。 預設值為 **2147483647**。 **0** 的值表示處理所有資料列之後的單一認可作業。|  
|FastLoadOptions|String|快速載入選項的集合。 快速載入選項包括資料表的鎖定和條件約束的檢查。 您可以指定其中一個選項、兩個選項或不指定任何選項。<br /><br /> 注意：雖然您無法在 [Excel 目的地編輯器] 中使用這個屬性的某些選項，但是可以使用 [進階編輯器] 來設定這些選項。|  
|[OpenRowset]|String|當 AccessMode 為 **OpenRowset**時，就是 Excel 目的地所存取之資料表或檢視表的名稱。|  
|OpenRowsetVariable|String|當 AccessMode 為 [從變數 OpenRowset] 時，就是包含 Excel 目的地所存取之資料表或檢視表名稱的變數名稱。|  
|SqlCommand|String|當 AccessMode 為 [SQL 命令] 時，就是 Excel 目的地用來指定資料之目的地資料行的 Transact-SQL 陳述式。|  
  
 Excel 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Excel 目的地](../../integration-services/data-flow/excel-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
 [使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)
  
  
