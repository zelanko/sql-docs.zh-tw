---
title: CreateRecordset 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 791586badfeff0c1bde35b5cdf25ba750f79fe80
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779026"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 方法 (RDS)
建立空的中斷[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>參數  
 *物件*  
 物件變數，表示[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)或[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *ColumnsInfos*  
 A **Variant**的定義中的每個資料行的屬性陣列**資料錄集**建立。 每個資料行定義包含四個必要的屬性和一個選擇性屬性的陣列。  
  
|attribute|描述|  
|---------------|-----------------|  
|名稱|資料行標頭的名稱。|  
|類型|資料類型的整數。|  
|大小|以字元為單位，無論何種資料類型寬度的整數。|  
|Null 屬性|布林值。|  
|小數位數 （選擇性）|這個選擇性屬性定義的小數位數的數字欄位。 如果未指定此值，數值會被截斷為小數位數的三個。 有效位數不受影響，但小數點的數字數目將會被截斷為 3。|  
  
 一組資料行陣列接著會分組成陣列，定義**資料錄集**。  
  
## <a name="remarks"></a>備註  
 伺服器端商務物件可以填入產生**資料錄集**與非-OLE DB 資料提供者的資料，例如作業系統檔案包含的股票報價。  
  
 下表列出[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)所支援的值**CreateRecordset**方法。 所列的號碼是用來定義欄位的參考編號。  
  
 每一個資料類型是固定的長度或可變長度。 固定長度類型應該定義大小為 – 1，，因為系統會預先決定大小，但仍需要大小定義。 可變長度資料類型可讓從 1 到 32767 之間的大小。  
  
 針對某些變數資料類型，類型可以強制轉型到替代資料行中指出的類型。 您將不會看到替代項目直到之後**資料錄集**建立及填入。 然後您可以檢查實際的資料類型，如有必要。  
  
|長度|常數|Number|Substitution|  
|------------|--------------|------------|------------------|  
|固定|**adTinyInt**|16||  
|固定|**adSmallInt**|2||  
|固定|**adInteger**|3||  
|固定|**adBigInt**|20||  
|固定|**adUnsignedTinyInt**|17||  
|固定|**adUnsignedSmallInt**|18||  
|固定|**adUnsignedInt**|19||  
|固定|**adUnsignedBigInt**|21||  
|固定|**adSingle**|4||  
|固定|**adDouble**|5||  
|固定|**adCurrency**|6||  
|固定|**adDecimal**|14||  
|固定|**adNumeric**|131||  
|固定|**adBoolean**|11||  
|固定|**adError**|10||  
|固定|**adGuid**|72||  
|固定|**adDate**|7||  
|固定|**adDBDate**|133||  
|固定|**adDBTime**|134||  
|固定|**adDBTimestamp**|135|7|  
|變數|**adBSTR**|8|130|  
|變數|**adChar**|129|200|  
|變數|**adVarChar**|200||  
|變數|**adLongVarChar**|201|200|  
|變數|**adWChar**|130||  
|變數|**adVarWChar**|202|130|  
|變數|**adLongVarWChar**|203|130|  
|變數|**adBinary**|128||  
|變數|**adVarBinary**|204||  
|變數|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>另請參閱  
 [CreateRecordset 方法範例 (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 方法範例 (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



