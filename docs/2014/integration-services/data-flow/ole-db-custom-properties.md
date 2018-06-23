---
title: OLE DB 自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a4c29542fe95e7f7323ac7d8975f391ba97ea274
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033680"
---
# <a name="ole-db-custom-properties"></a>OLE DB 自訂屬性
  **來源自訂屬性**  
  
 OLE DB 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 OLE DB 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用來存取資料庫的模式。 可能的值為**Open Rowset**，**來自變數的開啟資料列集**， `SQL Command`，和**來自變數的 SQL 命令**。 預設值為 **[開啟資料列集]**。|  
|AlwaysUseDefaultCodePage|布林|值，指出是否要使用的值`DefaultCodePage`每個資料行，還是嘗試中衍生字碼頁從每個資料行的地區設定的屬性。 這個屬性的預設值是`False`。|  
|CommandTimeout|Integer|命令逾時之前的秒數。值為 0 表示無限逾時。<br /><br /> 注意：雖然您無法在 [OLE DB 來源編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|DefaultCodePage|Integer|無法從資料來源中取得字碼頁資訊時要使用的字碼頁。|  
|[OpenRowset]|String|用來開啟資料列集之資料庫物件的名稱。|  
|OpenRowsetVariable|String|變數，其中包含用來開啟資料列集之資料庫物件的名稱。|  
|ParameterMapping|String|從 SQL 命令中的參數到變數的對應。|  
|SqlCommand|String|要執行的 SQL 命令。|  
|SqlCommandVariable|String|變數，其中包含要執行的 SQL 命令。|  
  
 OLE DB 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [OLE DB Source](ole-db-source.md)。  
  
 **目的地自訂屬性**  
  
 OLE DB 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 OLE DB 目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
> [!NOTE]  
>  這裡列出 （FastLoadKeepIdentity、 FastLoadKeepNulls 和 FastLoadOptions） 的 FastLoad 選項對應至所公開的類似的具名屬性`IRowsetFastLoad`Microsoft OLE DB 提供者所實作的 SQL Server (SQLOLEDB) 介面。 如需詳細資訊，請在 MSDN Library 中搜尋 IRowsetFastLoad。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定目的地如何存取其目的地資料庫。<br /><br /> 此屬性可以有下列其中一個值：<br /><br /> `OpenRowset` (0): 提供的資料表或檢視表名稱。<br />`OpenRowset from Variable` (1): 提供包含資料表或檢視名稱變數名稱。<br />`OpenRowset Using Fastload` (3): 提供的資料表或檢視表名稱。<br />`OpenRowset Using Fastload from Variable` (4): 提供包含資料表或檢視名稱變數名稱。<br />`SQL Command` (2): 提供的 SQL 陳述式。|  
|AlwaysUseDefaultCodePage|布林|值，指出是否要使用的值`DefaultCodePage`每個資料行，還是嘗試中衍生字碼頁從每個資料行的地區設定的屬性。 這個屬性的預設值是`False`。|  
|CommandTimeout|Integer|逾時之前 SQL 命令可以執行的秒數上限。值為 0 指出無限的時間。 這個屬性的預設值為 0。<br /><br /> 注意：雖然您無法在 [OLE DB 目的地編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|DefaultCodePage|Integer|與 OLE DB 目的地相關聯的預設字碼頁。|  
|FastLoadKeepIdentity|布林|一個值，指定載入資料時是否要複製識別值。 這個屬性只能搭配其中一個快速載入選項使用。 這個屬性的預設值是`False`。 此屬性會對應至 OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)屬性`SSPROP_FASTLOADKEEPIDENTITY`。|  
|FastLoadKeepNulls|布林|一個值，指定載入資料時是否要複製 Null 值。 這個屬性只能搭配其中一個快速載入選項使用。 這個屬性的預設值是`False`。 此屬性會對應至 OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)屬性`SSPROP_FASTLOADKEEPNULLS`。|  
|FastLoadMaxInsertCommitSize|Integer|一個值，指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **0**表示處理所有資料列之後的單一認可作業。|  
|FastLoadOptions|String|快速載入選項的集合。 快速載入選項包括資料表的鎖定和條件約束的檢查。 您可以指定其中一個選項、兩個選項或不指定任何選項。 此屬性會對應至 OLE DB IRowsetFastLoad 屬性`SSPROP_FASTLOADOPTIONS`和接受字串選項，例如`CHECK_CONSTRAINTS`和`TABLOCK`。<br /><br /> 注意：雖然您無法在 [Excel 目的地編輯器] 中使用這個屬性的某些選項，但是可以使用 [進階編輯器] 來設定這些選項。|  
|[OpenRowset]|String|當 AccessMode 是`OpenRowset`，資料表或檢視 OLE DB 目的地所存取的名稱。|  
|OpenRowsetVariable|String|當 AccessMode 是`OpenRowset from Variable`，包含名稱的資料表或檢視 OLE DB 目的地所存取的變數名稱。|  
|SqlCommand|String|當 AccessMode 是`SQL Command`，OLE DB 目的地會使用指定的資料的目的地資料行的 TRANSACT-SQL 陳述式。|  
  
 OLE DB 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [OLE DB Destination](ole-db-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  